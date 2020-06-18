### API (beta)

Accepted Content Types: `application/json` or `x-www-form-urlencoded`.

By default every json response is automatically escaped, therefore a `<` would become a `\u003c`.
You can pass the parameter `unescape_json` to any request to unescape the response json. Be careful though, as the resulting response might not be secure to embed into a document. So be sure to escape the string again whenever you're using it in front-end.

ref: https://hackerone.com/reports/47280

Example:
```
<script>
//<![CDATA[
var json={"</script><script>alert(1)//":"xss"}
//]]>
</script>
```

Beware all responses are `application/json` (with body).

#### Authentication

Each request must pass a private API key via the `ApiKey` header.
Public API keys are accepted only on `POST /public/consent` endpoint.

### Consent

#### List Consents

```
GET /beta/consent
```

Examples: [cURL](api/beta/curl.md#get-consent) | [PHP](api/beta/php.md#get-consent)

```json
# 200 OK
[{
    "id": "b04c4b2b-80b7-439f-8997-ade3d35cbb95",
    "timestamp": "2018-06-04T08:11:34.000+00:00",
    "owner": "521686",
    "source": "private",
    "subject": {
      "id": "0e371678-634a-4016-83ce-9b7c36f828e6",
      "email": "83ce_634a_4016_9b7c36f828e6_0e371678@example.com",
      "first_name": "Kianna",
      "last_name": "Fahey",
      "full_name": "Kianna Fahey",
      "verified": false
    },
    "consent_type": "cookie_policy",
    "preferences": {
      "newsletter": false
    }
  },
  {
    "id": "ee6644ea-08e9-4aaa-a7a9-18602731a123",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "681109",
    "source": "public",
    "subject": {
      "id": "8c6d1b71-0908-4604-948f-2f706500b5b1",
      "email": "0908.8c6d1b71.2f706500b5b1.4604.948f@example.org",
      "first_name": "Eleanora",
      "last_name": "Adams",
      "full_name": "Eleanora Adams",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "newsletter": true
    }
  },
  {
    "id": "e7a9f5db-481e-4c80-ac7d-a35e35d37f98",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "178473",
    "source": "private",
    "subject": {
      "id": "d084ab70-0460-4523-94b2-44841055b49c",
      "email": "94b2_4523_44841055b49c_0460_d084ab70@example.com",
      "first_name": "Abbie",
      "last_name": "Heidenreich",
      "full_name": "Abbie Heidenreich",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "third_party": true
    }
  },
  {
    "id": "e3481085-296c-4b11-a999-73d5d1309128",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "393753",
    "source": "private",
    "subject": {
      "id": "be8ca546-150d-4a6e-b2ac-ef76fb8a279e",
      "email": "b2ac_ef76fb8a279e_150d_4a6e_be8ca546@example.net",
      "first_name": "Grace",
      "last_name": "Dooley",
      "full_name": "Grace Dooley",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "another_preference_key": false,
      "newsletter": false
    }
  },
  {
    "id": "e1be0320-a854-4b01-a468-49b1752ee4f3",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "629879",
    "source": "public",
    "subject": {
      "id": "f8878254-c7ae-4169-b474-19e90d7b2f4f",
      "email": "f8878254_b474_19e90d7b2f4f_4169_c7ae@example.net",
      "first_name": "Providenci",
      "last_name": "Kulas",
      "full_name": "Providenci Kulas",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "newsletter": false,
      "random_preference_key": true,
      "third_party": true,
      "another_preference_key": false
    }
  },
  {
    "id": "cbe2bba8-d31d-4a27-9e2d-b38de4f22a68",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "989797",
    "source": "public",
    "subject": {
      "id": "6387dc5d-d474-4da8-8c40-8b197dee8d7c",
      "email": "6387dc5d.4da8.d474.8c40.8b197dee8d7c@example.com",
      "first_name": "Alan",
      "last_name": "Rutherford",
      "full_name": "Alan Rutherford",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "newsletter": true,
      "random_preference_key": true
    }
  },
  {
    "id": "ca429c28-e1cd-4b95-87ae-48adb8fe56bb",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "885846",
    "source": "public",
    "subject": {
      "id": "b2ad578d-0aa9-4bd5-becd-e2e7a2019e7a",
      "email": "b2ad578d.becd.e2e7a2019e7a.0aa9.4bd5@example.net",
      "first_name": "Ruby",
      "last_name": "Lemke",
      "full_name": "Ruby Lemke",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "third_party": true,
      "random_preference_key": false
    }
  },
  {
    "id": "bf12770e-840a-40cd-ab79-5d88576b6b73",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "369168",
    "source": "public",
    "subject": {
      "id": "d4f24d92-56c2-4372-8696-fec829da5ccc",
      "email": "fec829da5ccc.8696.4372.56c2.d4f24d92@example.com",
      "first_name": "Hank",
      "last_name": "Klein",
      "full_name": "Hank Klein",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "newsletter": false
    }
  },
  {
    "id": "b489e2d4-2fc6-44e1-ba54-e5f81000d30a",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "781022",
    "source": "public",
    "subject": {
      "id": "38bc623f-b386-4b66-8ee6-5e7d91c19800",
      "email": "38bc623f.8ee6.4b66.5e7d91c19800.b386@example.net",
      "first_name": "Kamren",
      "last_name": "Pacocha",
      "full_name": "Kamren Pacocha",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "newsletter": true
    }
  },
  {
    "id": "b2ec7aa8-35e7-470c-8b51-bd39fa686a3a",
    "timestamp": "2018-06-04T08:11:33.000+00:00",
    "owner": "527898",
    "source": "public",
    "subject": {
      "id": "0cc94c66-d9eb-4ace-af3d-1d48fba265f9",
      "email": "1d48fba265f9_4ace_af3d_d9eb_0cc94c66@example.net",
      "first_name": "Maryjane",
      "last_name": "Wiegand",
      "full_name": "Maryjane Wiegand",
      "verified": false
    },
    "consent_type": null,
    "preferences": {
      "newsletter": true
    }
  }
]
```

##### Accepted query parameters:

| Name                |          | Value   | Description | Default value |
| ------------------- | -------- | ------- | ----------- | ------------- |
| from_time           | optional | String  | Filter by consents timestamp. Returns all consents from that time onward (inclusive). Valid formats: 2018-02-22 00:40:00 UTC, 2018-02-22T00:40:00Z (ISO 8601), 1519260000 (unix timestamp in seconds). | null |
| to_time             | optional | String  | Filter by consents timestamp. Returns all consents from that time backward (inclusive). Valid formats: 2018-02-22 00:40:00 UTC, 2018-02-22T00:40:00Z (ISO 8601), 1519260000 (unix timestamp in seconds). | null |
| source              | optional | String  | Filter by consents source. Possible values: public, private. | null |
| ip_address          | optional | String  | Filter by IP address. Default null. Valid formats (IP address format) | 'none' |
| consent_type        | optional | String  | Filter by consents type. By not passing this value it returns all consents. Possible values: cookie_policy, null. | not passed |
| subject_id          | optional | String  | Filter by Subject ID. | null |
| subject_email_exact | optional | String  | Filter by Subject email. It must exactly match (case sensitive). | null |
| subject_email       | optional | String  | Filter by Subject email. It tries to match parts of the provided email split by dots and spaces. Ex. providing "@test.com" will match all the subjects with an email containing "@test" or containing "com" (case insensitive). | null |
| subject_first_name  | optional | String  | Filter by Subject first name. It must exactly match (case sensitive). | null |
| subject_last_name   | optional | String  | Filter by Subject last name. It must exactly match (case sensitive). | null |
| subject_full_name   | optional | String  | Filter by Subject full name. It tries to match parts of the provided full name split by dots and spaces. Ex. "test hello" will match all the subjects with a full name containing "test" or containing "hello" (case insensitive). | null |
| subject_verified    | optional | Boolean  | Filter by subject verified status. Possible values: true, false. | null |
| preference_key      | optional | String  | Filter for consents in which the key exists. | null |
| fulltext            | optional | String  | Filters for results with the value provided being contained in either subject's id, first_name, last_name, full_name, email. | null |
| starting_after      | optional | String  | Cursor which indicates after which Consent the results should be returned (cursor excluded). | null |
| limit               | optional | Numeric | Number indicating the number of results returned. Min: 1, Max: 101. | 10 |

This method supports cursor-based pagination via the `starting_after` parameter. This paramater takes an existing Consent and returns objects after it.


#### Get a Consent

```
GET /beta/consent/:id
```

Examples: [cURL](api/beta/curl.md#get-consentid) | [PHP](api/beta/php.md#get-consentid)

```json
# 200 OK
{
  "id": "de801ca9-abec-45e2-8f7c-729822cfffad",
  "timestamp": "2018-05-04T14:52:26Z",
  "checksum": "336dd0c5ee2253794b8cca6ee2b2fec835ab25a7097c4405014d02e4ffe4d5e5",
  "owner": "1",
  "subject": {
    "id": "custom_subject_id",
    "owner_id": "1",
    "email": "subject@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "verified": false
  },
  "preferences": {
    "privacy_policy": true,
    "newsletter": false
  },
  "legal_notices": [
    {
      "identifier": "privacy_policy",
      "version": 123
    },
    {
      "identifier": "terms_and_conditions",
      "version": 123
    }
  ],
  "proofs": [
    {
      "content": "proof_1",
      "form": "proof_1 form"
    },
    {
      "content": "proof_2",
      "form": "proof_2 form"
    }
  ],
  "ip_address": null,
  "consent_type": null
}
```

Beware `legal_notices`'s `version` is normalized on beta channel, but it's not on current channel as this would potentially be a breaking change. We decided not to merge it into current.

Eg. current

```json
"legal_notices": [
  {
    "identifier": "privacy_policy",
    "version": "123.0"
  }
]
```

Eg. beta

```json
"legal_notices": [
  {
    "identifier": "privacy_policy",
    "version": 123
  }
]
```

#### Create a Consent

```json
POST /beta/consent
{
  "subject": {
    "id": "testsubject",
    "email": "subject@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "verified": false
  },
  "legal_notices": [
    {
      "identifier": "privacy_policy",
      "version": 123
    },
    {
      "identifier": "terms_and_conditions",
      "version": 123
    }
  ],
  "proofs": [
    {
      "content": "proof_1",
      "form": "proof_1 form",
    },
    {
      "content": "proof_2",
      "form": "proof_2 form"
    }
  ],
  "preferences": {
    "newsletter": false,
    "privacy_policy": true
  },
  "ip_address": "127.0.0.1",
  "consent_type": "cookie_policy"
}
```

Examples: [cURL](api/beta/curl.md#post-consent) | [PHP](api/beta/php.md#post-consent)

```json
# 200 OK
{
  "id": "de801ca9-abec-45e2-8f7c-729822cfffad",
  "timestamp": "2018-05-04T14:52:26Z",
  "subject_id": "testsubject"
}
```

### Subjects

#### List Subjects

```
GET /beta/subjects
```

Examples: [cURL](api/beta/curl.md#get-subjects) | [PHP](api/beta/php.md#get-subjects)

```json
# 200 OK
[
  {
    "id": "d2a55da5-0777-4625-94bd-b69948703e71",
    "owner_id": "131132",
    "email": "rath.jorge@example.com",
    "first_name": "Jorge",
    "last_name": "Rath",
    "full_name": "Jorge Rath",
    "preferences": null,
    "verified": true,
    "timestamp": "2018-09-12T16:22:21+00:00"
  },
  {
    "id": "b75c6d0c-550f-4f84-9e92-2f351d481220",
    "owner_id": "131132",
    "email": "aufderhar_alfonso@example.net",
    "first_name": "Alfonso",
    "last_name": "Aufderhar",
    "full_name": "Alfonso Aufderhar",
    "preferences": null,
    "verified": true,
    "timestamp": "2018-09-12T16:22:21+00:00"
  },
  {
    "id": "a9c8c720-cb07-4a52-81c3-7cb7fb4f877e",
    "owner_id": "131132",
    "email": "vandervort.furman@example.net",
    "first_name": "Furman",
    "last_name": "Vandervort",
    "full_name": "Furman Vandervort",
    "preferences": null,
    "verified": true,
    "timestamp": "2018-09-12T16:22:21+00:00"
  },
  {
    "id": "6ccc2802-3bcb-49af-a4c5-14dc89ba94bc",
    "owner_id": "131132",
    "email": "alvis.rohan@example.org",
    "first_name": "Alvis",
    "last_name": "Rohan",
    "full_name": "Alvis Rohan",
    "preferences": null,
    "verified": true,
    "timestamp": "2018-09-12T16:22:21+00:00"
  },
  {
    "id": "5900f856-619e-42b0-92a5-b2ebd016ac01",
    "owner_id": "131132",
    "email": "brown.marlee@example.net",
    "first_name": "Marlee",
    "last_name": "Brown",
    "full_name": "Marlee Brown",
    "preferences": null,
    "verified": true,
    "timestamp": "2018-09-12T16:22:21+00:00"
  }
]
```

##### Accepted query parameters:

| Name           |          | Value   | Description | Default value |
| -------------- | -------- | ------- | ----------- | ------------- |
| id             | optional | String  | Filter by id. It must exactly match. | null |
| owner_id       | optional | String  | Filter by owner_id. It must exactly match. | null |
| email_exact    | optional | String  | Filter by email. It must exactly match (case sensitive). | null |
| email          | optional | String | Filter by email. It tries to match parts of the provided email split by dots and spaces. Ex. providing "@test.com" will match all the subjects with an email containing "@test" or containing "com" (case insensitive). | null |
| first_name     | optional | String | Filter by first name. It must exactly match (case sensitive). | null |
| last_name      | optional | String | Filter by last name. It must exactly match (case sensitive). | null |
| full_name      | optional | String | Filter by full name. It tries to match parts of the provided full name split by dots and spaces. Ex. "test hello" will match all the subjects with a full name containing "test" or containing "hello" (case insensitive). | null |
| from_time      | optional | String  | Filter by subjects timestamp. Returns all subjects from that time onward (inclusive). Valid formats: 2018-02-22 00:40:00 UTC, 2018-02-22T00:40:00Z (ISO 8601), 1519260000 (unix timestamp in seconds). | null |
| to_time        | optional | String  | Filter by subjects timestamp. Returns all subjects from that time backward (inclusive). Valid formats: 2018-02-22 00:40:00 UTC, 2018-02-22T00:40:00Z (ISO 8601), 1519260000 (unix timestamp in seconds). | null |
| verified       | optional | Boolean | Filter by verified status. Possible values: true, false. | null |
| fulltext       | optional | String  | Filters for results with the value provided being contained in either id, first_name, last_name, full_name, email. | null |
| starting_after | optional | String | Cursor which indicates after which Subject the results should be returned (cursor excluded). | null |
| limit          | optional | Numeric | Number indicating the number of results returned. Min: 1, Max: 101. | 10 |

This method supports cursor-based pagination via the `starting_after` parameter. This paramater takes an existing Subject and returns objects after it.

#### Get a Subject

```
GET /beta/subjects/:id
```

Examples: [cURL](api/beta/curl.md#get-subjectsid) | [PHP](api/beta/php.md#get-subjectsid)

```json
# 200 OK
{
  "id": "testsubject",
  "owner_id": "1",
  "email": "subject@example.com",
  "first_name": "John",
  "last_name": "Doe",
  "verified": false,
  "preferences": {
    "privacy_policy": {
      "value": true,
      "consent_id": "de801ca9-abec-45e2-8f7c-729822cfffad"
    },
    "newsletter": {
      "value": true,
      "consent_id": "de801ca9-abec-45e2-8f7c-729822cfffad"
    }
  }
}
```

#### Create a Subject

```json
POST /beta/subjects
{
  "id": "testsubject",
  "email": "subject@example.com",
  "first_name": "John",
  "last_name": "Doe",
  "full_name": "John Doe",
  "verified": false
}
```

Examples: [cURL](api/beta/curl.md#post-subjects) | [PHP](api/beta/php.md#post-subjects)

```json
# 200 OK
{
  "id": "testsubject",
  "created_at": "2018-05-04T14:52:26Z"
}
```

#### Update a Subject

```json
PUT|PATCH /beta/subjects/:id
{
  "first_name": "Mary",
  "verified": true
}
```

Examples: [cURL](api/beta/curl.md#patch-subjectsid) | [PHP](api/beta/php.md#patch-subjectsid)

```json
# 200 OK
{
  "id": "testsubject",
  "created_at": "2018-05-04T14:52:26Z"
}
```

### Legal Notices

#### List Legal Notices

```
GET /beta/legal_notices
```

Examples: [cURL](api/beta/curl.md#get-legal_notices) | [PHP](api/beta/php.md#get-legal_notices)

```json
# 200 OK
[
  {
    "id": "0_cookie_policy",
    "owner_id": "0",
    "identifier": "cookie_policy",
    "version": 20,
    "timestamp": "2018-10-09T12:38:04Z",
    "content": {
      "en": "Et vinculum clam decerno arguo admoveo velum sponte tot suppellex venustas defendo dolor decumbo est.",
      "it": "Collum tutis esse confugo porro urbs varius abscido turpis decor praesentium tardus voluptate fugit numquam."
    }
  },
  {
    "id": "0_terms",
    "owner_id": "0",
    "identifier": "terms",
    "version": 19,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Venia valde vel surculus capitulus adfectus patior comparo acsi cur vero super cursim.",
      "it": "Consuasor arcesso conscendo crudelis cauda aer aut adeptio illo argentum comis subiungo subito colo."
    }
  },
  {
    "id": "0_cookie_policy",
    "owner_id": "0",
    "identifier": "cookie_policy",
    "version": 18,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Ullus voco aufero speculum fugiat audacia laboriosam vilicus amita trans aut ut.",
      "it": "Alo veritatis ipsa tristis cuius occaecati adflicto creta verecundia facere solvo despirmatio cupiditate crinis aqua bos."
    }
  },
  {
    "id": "0_privacy_policy",
    "owner_id": "0",
    "identifier": "privacy_policy",
    "version": 17,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Confero succedo caelum adhaero quo vir deorsum quaerat utor sit ustulo cribro.",
      "it": "Bibo cubitum unus est ambitus contego apparatus alo via abutor utroque xiphias voco."
    }
  },
  {
    "id": "0_privacy_policy",
    "owner_id": "0",
    "identifier": "privacy_policy",
    "version": 16,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Qui porro culpo attero benevolentia aut sed sulum adfero artificiose adsidue tam amo validus vel spectaculum.",
      "it": "Cerno ipsum fugit compello cursim ter surgo asporto debilito excepturi adversus facere."
    }
  },
  {
    "id": "0_terms",
    "owner_id": "0",
    "identifier": "terms",
    "version": 15,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Tunc timidus veritatis maiores advenio aperio testimonium defluo celo cuius adsuesco deripio.",
      "it": "Depulso dignissimos vinitor curatio caelestis cedo et sum concedo id admoneo appositus."
    }
  },
  {
    "id": "0_terms",
    "owner_id": "0",
    "identifier": "terms",
    "version": 14,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Repellat mollitia desidero videlicet est textilis stips nisi aequus solum depromo agnitio usus.",
      "it": "Vomito tonsor comitatus illum aut usitas laboriosam canonicus tepesco benigne confugo trado."
    }
  },
  {
    "id": "0_cookie_policy",
    "owner_id": "0",
    "identifier": "cookie_policy",
    "version": 13,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Temperantia alias somniculosus absorbeo utique caecus terror demitto trucido desidero baiulus sublime.",
      "it": "Perspiciatis at tredecim curriculum comprehendo deduco corrupti attonbitus barba cruentus communis comparo thorax cauda spero vito anser."
    }
  },
  {
    "id": "0_cookie_policy",
    "owner_id": "0",
    "identifier": "cookie_policy",
    "version": 12,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Allatus cena surculus ventito ver adversus torrens demo venustas toties veritas qui cado vis.",
      "it": "Talio avoco aptus compono et subiungo peior bellum depromo aureus torqueo adeptio nobis."
    }
  },
  {
    "id": "0_terms",
    "owner_id": "0",
    "identifier": "terms",
    "version": 11,
    "timestamp": "2018-10-09T12:38:03Z",
    "content": {
      "en": "Aliquam cubicularis tergum utor cinis concido ratione vociferor uter deduco tertius verecundia alo claustrum sto vos aegrotatio.",
      "it": "Corona ut comes sub coaegresco caute casus laboriosam tremo vulariter aegrotatio pauci callide assentator basium."
    }
  }
]
```

##### Accepted query parameters:

| Name                      |          | Value   | Description |
| ------------------------- | -------- | ------- | ----------- |
| id                        | optional | String  | Filter by id. It must exactly match. Default null |
| identifier                | optional | String  | Filter by identifier. It must exactly match (case sensitive). Default null |
| version                   | optional | Numeric | Filter by version. It must exactly match. Default null |
| language                  | optional | String  | Filter by legal notices which contents include the specified language (using short form like 'en', 'it' etc.). Default null |
| from_time                 | optional | String  | Filter by legal notices timestamp. Returns all legal notices from that time onward (inclusive). Valid formats: 2018-02-22 00:40:00 UTC, 2018-02-22T00:40:00Z (ISO 8601), 1519260000 (unix timestamp in seconds). Default null |
| to_time                   | optional | String  | Filter by legal notices timestamp. Returns all legal notices from that time backward (inclusive). Valid formats: 2018-02-22 00:40:00 UTC, 2018-02-22T00:40:00Z (ISO 8601), 1519260000 (unix timestamp in seconds). Default null |
| starting_after_version    | optional | Numeric | Cursor which indicates after which Legal Notice's version the results should be returned (cursor excluded). Default null |
| starting_after_identifier | optional | String | Cursor which indicates after which Legal Notice's identifier the results should be returned (cursor excluded). Default null |
| limit                     | optional | Numeric | Number indicating the number of results returned. Min: 1, Max: 101. Default 10 |

This method supports cursor-based pagination via the `starting_after_version` and `starting_after_identifier` parameters. These paramaters take an existing Legal Notice and return objects after it. Both parameters are required in order to paginate.

#### Create a Legal Notice

```json
POST /beta/legal_notices
{
  "identifier": "privacy_policy",
  "content": "privacy policy content",
  "timestamp": "2018-05-16T13:55:57Z"
}
```

Examples: [cURL](api/beta/curl.md#post-legal_notices) | [PHP](api/beta/php.md#post-legal_notices)

##### with multi-language content

```json
POST /beta/legal_notices
{
  "identifier": "privacy_policy",
  "content": {
    "en": "privacy policy content",
    "it": "contenuto della privacy policy"
  },
  "timestamp": "2018-05-16T13:55:57Z"
}
```

```json
# 200 OK
{
  "identifier": "privacy_policy",
  "timestamp": "2018-05-16T13:55:57Z",
  "version": 1
}
```

#### Create multiple Legal Notices

```json
POST /beta/legal_notices
[
  {
    "identifier": "privacy_policy",
    "content": "privacy policy content",
    "timestamp": "2018-05-16T13:55:57Z"
  },
  {
    "identifier": "cookie_policy",
    "content": "cookie policy content",
    "timestamp": "2018-05-16T13:55:57Z"
  }
]
```

```json
# 200 OK
[
  {
    "identifier": "privacy_policy",
    "timestamp": "2018-05-16T13:55:57Z",
    "version": 1
  },
  {
    "identifier": "cookie_policy",
    "timestamp": "2018-05-16T13:55:57Z",
    "version": 1
  }
]
```

### Get a Legal Notice version

```
GET /beta/legal_notices/:identifier/:version
```

Examples: [cURL](api/beta/curl.md#get-legal_noticesidentifierversion) | [PHP](api/beta/php.md#get-legal_noticesidentifierversion)

```json
# 200 OK
{
  "identifier": "privacy_policy",
  "version": 3,
  "timestamp": "2018-05-16T13:55:57Z",
  "content": "privacy policy content"
}
```

### Get all Legal Notice versions

```
GET /legal_notices/:identifier
```

Examples: [cURL](api/beta/curl.md#get-legal_noticesidentifier) | [PHP](api/beta/php.md#get-legal_noticesidentifier)

##### Accepted query parameters:

| Name           |          | Value  | Description | Default value |
| ----           | -        | -----  | ----------- | ------------- |
| limit          | optional | Number | Limit the number of results. | 10 |
| starting_after | optional | Number | Cursor to be used for pagination. | null |

This method supports cursor-based pagination via the `starting_after` parameter. This paramater takes an existing Legal Notice version and returns objects in reverse order.

```json
# 200 OK
[
  {
    "identifier": "privacy_policy",
    "version": 3,
    "timestamp": "2018-05-16T13:55:57Z",
    "id": "1234_privacy_policy",
    "owner_id": "1234",
    "content": "privacy policy content"
  },
  {
    "identifier": "privacy_policy",
    "version": 2,
    "timestamp": "2018-03-16T13:55:57Z",
    "id": "1234_privacy_policy",
    "owner_id": "1234",
    "content": "privacy policy content"
  },
  {
    "identifier": "privacy_policy",
    "version": 1,
    "timestamp": "2018-01-16T13:55:57Z",
    "id": "1234_privacy_policy",
    "owner_id": "1234",
    "content": "privacy policy content"
  }
]
```
