# GDPR Consent API

[![CircleCI](https://circleci.com/gh/iubenda/consents_api/tree/master.svg?style=shield&circle-token=4d54e963921d1b10f06dd9606ff0111cda6d047a)](https://circleci.com/gh/iubenda/consents_api/tree/master)


### API

[See API docs (stable)](docs/API_stable.md)
[See API docs (beta)](docs/API_beta.md)

### Requirements

* Ruby v2.5
* Redis (for sidekiq)
* MongoDB
* Kong
* MinIO

#### MongoDB

Tables:
* `consents` hash_key: `id`
* `subjects` hash_key: `id`, range_key: `owner_id`
* `legal_notices` hash_key: `id`, range_key: `version`
* `binary_documents` hash_key: `id`
  * `parent_id-index` GSI hash_key: `parent_id`, range_key: `parent_type`
  * `owner_id-index` GSI hash_key: `owner_id`

#### Elasticsearch

Indexes:
* `consent`
* `subject`
* `legal_notice`

### Development

#### Credentials

The `master.key` can be found on 1P in the vault `Sysadmin` under the name of `Consents API master.key`

#### Kong

Kong is not required for development. When not proxying requests through Kong, each request should contain `X-CONSUMER-CUSTOM-ID` header with the following value: `private_xxx` (change `xxx` with any owner ID you want).

To use Kong as a Proxy:

1. start Kong VM
```console
user@host:consents_api$ cd kong_vagrant && vagrant up
```
2. Configure and seed Kong
```console
user@host:consents_api$ rake kong:configure
user@host:consents_api$ rake kong_development:seed
```
`rake kong_development:seed` will output a private and a public API key. Pass the private key via the `APIKEY` header.

Kong listens on port `8000` and is configured to proxy the requests to the host machine on port `3000`, hence the Consent API Rails application should listen on `0.0.0.0:3000`.
Finally, if you want to proxy the requests via Kong, use `localhost:8000`, instead of `localhost:3000`.

All requests to the API proxied by Kong, must have the `ApiKey` header.
Once the request is authenticated, Kong will set `X-CONSUMER-CUSTOM-ID` header containing the authenticated Owner ID and forward the request to the backend application.
If unauthenticated, Kong will respond with `401` / `403` status and not forward the request to the upstream.

#### MinIO

The default port is 9000 and if you're using the development-kit then you have an instance on 9000 and one on 10000 called minio and minio_test.

You have to create the buckets set up in `.env.development` and `.env.test` with policies permitting "read" on both prefixes of "backlog" and "store".

#### Rails

```console
user@host:consents_api$ bundle install
user@host:consents_api$ foreman start
```

Local MongoDB is listening on port `27017`.

### Testing

```console
user@host:consents_api$ bundle exec rspec
```

#### With Docker

```console
user@host:consents_api$ RAILS_ENV=test bundle exec rspec
```

#### With slow tests

By default the project is set up not to run slow tests (check `.rspec`). You can run all tests by appending `-O .rspec-no-tags` to your command as such:

```console
user@host:consents_api$ bundle exec rspec -O .rspec-no-tags
```

### Importing Data

#### Having an array of ids saved in a json file

Convert the file into a `keys_to_import` structure and then proceed with the beneath method.

```console
  file = File.read(path)
  array = JSON(file)

  array.in_groups_of(10_000, false) do |group|
    DataImport::KeysToImportConverter.new(group.map { |c_id| Consent.new(id: c_id) }).save_to_file!
  end
```

#### Having a `keys_to_import` structure

```console
  path = [YOUR PATH HERE]
  OR
  path = Rails.root.join('import_files', 'consent_import_DO_outage_30_01_2019.json')
  OR
  paths = Dir[Rails.root.join('migration_files/keys_to_import', 'consent', '*').to_s]
  paths.each do |path| ... end

  ImportDataToElasticSearchService.new('Consent', 'consent', read_capacity: 150, also_import_subjects: true, keys_to_import_json_filepath: path).call!
```

`[YOUR PATH HERE]` should be a path in `project/import_files` directory. It's a linked dir set in capistrano on `deploy.rb`. This way if a deploy happens in between you don't lose the uploaded file.
If you used the `KeysToImportConverter` then the path will be `project/migration_files/keys_to_import/[model]/{file}.json`

A maximum array size is set per single file in `DataImport::KeysToImportConverter`. Split json file's array accordingly.

### Setting up MongoDB

Enter mongodb console with privileges and:

```json
use consents_api_development;
db.createUser(
  {
    "user": "mongodb",
    "pwd": "mongodb",
    "roles": [
      { "role": "dbOwner", "db": "consents_api_development" }
    ],
    "mechanisms": [ "SCRAM-SHA-256" ]
  }
)

use consents_api_test;
db.createUser(
  {
    "user": "mongodb",
    "pwd": "mongodb",
    "roles": [
      { "role": "dbOwner", "db": "consents_api_test" }
    ],
    "mechanisms": [ "SCRAM-SHA-256" ]
  }
)
```
