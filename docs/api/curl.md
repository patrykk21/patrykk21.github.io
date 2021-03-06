### `POST /consent`

```console
$ curl https://consent.iubenda.com/consent \
  -X POST \
  -H "ApiKey: your-private-api-key" \
  -H "Content-Type: application/json" \
  -d  '{ "subject": { "id": "J02eZvKYlo2ClwuJ1", "email": "subject@example.com" }, "preferences": { "newsletter": true }, "legal_notices": [{ "identifier": "privacy_policy" }], "proofs": [{ "content": "proof_content", "form": "proof_form" }], "ip_address": "127.0.0.1" }'
```

##### response:

```json
{"id":"1dbbc6f8-6a57-4407-b687-d6e6f818742f","timestamp":"2018-06-06T09:48:44.265Z","subject_id":"J02eZvKYlo2ClwuJ1"}
```

### `GET /consent`

```console
$ curl https://consent.iubenda.com/consent/ \
  -H "ApiKey: your-private-api-key"
```

##### response:

```json
[{"id":"b04c4b2b-80b7-439f-8997-ade3d35cbb95","timestamp":"2018-06-04T08:11:34.000+00:00","owner":"12345","source":"private","subject":{"id":"0e371678-634a-4016-83ce-9b7c36f828e6","email":"83ce_634a_4016_9b7c36f828e6_0e371678@example.com","first_name":"Kianna","last_name":"Fahey","full_name":"Kianna Fahey","verified":false},"preferences":{"newsletter":false},"ip_address":"79.42.49.139"},{"id":"ee6644ea-08e9-4aaa-a7a9-18602731a123","timestamp":"2018-06-04T08:11:33.000+00:00","owner":"12345","source":"public","subject":{"id":"8c6d1b71-0908-4604-948f-2f706500b5b1","email":"0908.8c6d1b71.2f706500b5b1.4604.948f@example.org","first_name":"Eleanora","last_name":"Adams","full_name":"Eleanora Adams","verified":false},"preferences":{"newsletter":true},"ip_address":null},{"id":"bf12770e-840a-40cd-ab79-5d88576b6b73","timestamp":"2018-06-04T08:11:33.000+00:00","owner":"12345","source":"public","subject":{"id":"d4f24d92-56c2-4372-8696-fec829da5ccc","email":"fec829da5ccc.8696.4372.56c2.d4f24d92@example.com","first_name":"Hank","last_name":"Klein","full_name":"Hank Klein","verified":false},"preferences":{"newsletter":false},"ip_address":"79.42.49.139"}]
```

### `GET /consent/:id`

```console
$ curl https://consent.iubenda.com/consent/1dbbc6f8-6a57-4407-b687-d6e6f818742f \
  -H "ApiKey: your-private-api-key"
```

##### response:

```json
{"id":"1dbbc6f8-6a57-4407-b687-d6e6f818742f","timestamp":"2018-05-04T14:52:26Z","owner":"1","subject":{"id":"custom_subject_id","owner_id":"1","email":"subject@example.com","first_name":"John","last_name":"Doe","verified":false},"preferences":{"privacy_policy":true,"newsletter":false},"legal_notices":[{"identifier":"privacy_policy","version":"123.0"},{"identifier":"terms_and_conditions","version":"123.0"}],"proofs":[{"content":"proof_1","form":"proof_1 form"},{"content":"proof_2","form":"proof_2 form"}],"ip_address":null}
```

### `GET /subjects`

```console
$ curl https://consent.iubenda.com/subjects \
  -X GET \
  -H "ApiKey: your-private-api-key" \
  -H "Content-Type: application/json"
```

##### response:

```json
[{"id":"d2a55da5-0777-4625-94bd-b69948703e71","owner_id":"131132","email":"rath.jorge@example.com","first_name":"Jorge","last_name":"Rath","full_name":"Jorge Rath","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"b75c6d0c-550f-4f84-9e92-2f351d481220","owner_id":"131132","email":"aufderhar_alfonso@example.net","first_name":"Alfonso","last_name":"Aufderhar","full_name":"Alfonso Aufderhar","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"a9c8c720-cb07-4a52-81c3-7cb7fb4f877e","owner_id":"131132","email":"vandervort.furman@example.net","first_name":"Furman","last_name":"Vandervort","full_name":"Furman Vandervort","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"6ccc2802-3bcb-49af-a4c5-14dc89ba94bc","owner_id":"131132","email":"alvis.rohan@example.org","first_name":"Alvis","last_name":"Rohan","full_name":"Alvis Rohan","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"5900f856-619e-42b0-92a5-b2ebd016ac01","owner_id":"131132","email":"brown.marlee@example.net","first_name":"Marlee","last_name":"Brown","full_name":"Marlee Brown","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"}]
```

### `POST /subjects`

```console
$ curl https://consent.iubenda.com/subjects \
  -X POST \
  -H "ApiKey: your-private-api-key" \
  -H "Content-Type: application/json" \
  -d '{ "email": "john@example.com", "first_name": "John", "last_name": "Doe" }'
```

##### response:

```json
{"id":"9f5a50f6-052c-4595-8bc4-760dc05d86ba","timestamp":"2018-06-06T11:05:41.600Z"}
```


### `GET /subjects/:id`

```console
$ curl https://consent.iubenda.com/subjects/9f5a50f6-052c-4595-8bc4-760dc05d86ba \
  -H "ApiKey: your-private-api-key"
```

##### response:

```json
{"id":"9f5a50f6-052c-4595-8bc4-760dc05d86ba","owner_id":"123","email":"john@example.com","first_name":"John","last_name":"Doe","full_name":null,"preferences":null,"verified":false,"timestamp":"2018-06-06T11:05:41+00:00"}
```

### `PATCH /subjects/:id`

```console
$ curl https://consent.iubenda.com/subjects/9f5a50f6-052c-4595-8bc4-760dc05d86ba \
  -X PATCH \
  -H "ApiKey: your-private-api-key" \
  -H "Content-Type: application/json" \
  -d '{ "email": "mary@example.com", "first_name": "Mary", "last_name": "Doe" }'
```

##### response:

```json
{"id":"9f5a50f6-052c-4595-8bc4-760dc05d86ba","timestamp":"2018-06-06T11:05:41.000+00:00"}
```

### `POST /legal_notices`

```console
$ curl https://consent.iubenda.com/legal_notices \
  -X POST \
  -H "ApiKey: your-private-api-key" \
  -H "Content-Type: application/json" \
  -d '{ "identifier": "privacy_policy", "content": "privacy policy legal text" }'
```

##### response:

```json
{"identifier":"privacy_policy","version":1,"timestamp":"2018-06-06T15:56:10.090Z"}
```

### `GET /legal_notices`

```console
$ curl https://consent.iubenda.com/legal_notices \
  -H "ApiKey: your-private-api-key"
```

##### response:

```json
[{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":20,"timestamp":"2018-10-09T12:38:04Z","content":{"en":"Et vinculum clam decerno arguo admoveo velum sponte tot suppellex venustas defendo dolor decumbo est.","it":"Collum tutis esse confugo porro urbs varius abscido turpis decor praesentium tardus voluptate fugit numquam."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":19,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Venia valde vel surculus capitulus adfectus patior comparo acsi cur vero super cursim.","it":"Consuasor arcesso conscendo crudelis cauda aer aut adeptio illo argentum comis subiungo subito colo."}},{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":18,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Ullus voco aufero speculum fugiat audacia laboriosam vilicus amita trans aut ut.","it":"Alo veritatis ipsa tristis cuius occaecati adflicto creta verecundia facere solvo despirmatio cupiditate crinis aqua bos."}},{"id":"0_privacy_policy","owner_id":"0","identifier":"privacy_policy","version":17,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Confero succedo caelum adhaero quo vir deorsum quaerat utor sit ustulo cribro.","it":"Bibo cubitum unus est ambitus contego apparatus alo via abutor utroque xiphias voco."}},{"id":"0_privacy_policy","owner_id":"0","identifier":"privacy_policy","version":16,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Qui porro culpo attero benevolentia aut sed sulum adfero artificiose adsidue tam amo validus vel spectaculum.","it":"Cerno ipsum fugit compello cursim ter surgo asporto debilito excepturi adversus facere."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":15,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Tunc timidus veritatis maiores advenio aperio testimonium defluo celo cuius adsuesco deripio.","it":"Depulso dignissimos vinitor curatio caelestis cedo et sum concedo id admoneo appositus."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":14,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Repellat mollitia desidero videlicet est textilis stips nisi aequus solum depromo agnitio usus.","it":"Vomito tonsor comitatus illum aut usitas laboriosam canonicus tepesco benigne confugo trado."}},{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":13,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Temperantia alias somniculosus absorbeo utique caecus terror demitto trucido desidero baiulus sublime.","it":"Perspiciatis at tredecim curriculum comprehendo deduco corrupti attonbitus barba cruentus communis comparo thorax cauda spero vito anser."}},{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":12,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Allatus cena surculus ventito ver adversus torrens demo venustas toties veritas qui cado vis.","it":"Talio avoco aptus compono et subiungo peior bellum depromo aureus torqueo adeptio nobis."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":11,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Aliquam cubicularis tergum utor cinis concido ratione vociferor uter deduco tertius verecundia alo claustrum sto vos aegrotatio.","it":"Corona ut comes sub coaegresco caute casus laboriosam tremo vulariter aegrotatio pauci callide assentator basium."}}]
```

### `GET /legal_notices/:identifier/:version`

```console
$ curl https://consent.iubenda.com/legal_notices/privacy_policy/1 \
  -H "ApiKey: your-private-api-key"
```

##### response:

```json
{"identifier":"privacy_policy","version":1,"timestamp":"2018-06-06T15:56:10.000+00:00","content":"privacy policy legal text"}
```

### `GET /legal_notices/:identifier`

```console
$ curl https://consent.iubenda.com/legal_notices/privacy_policy \
  -H "ApiKey: your-private-api-key"
```

##### response:

```json
[{"identifier":"privacy_policy","version":3,"timestamp":"2018-05-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"},{"identifier":"privacy_policy","version":2,"timestamp":"2018-03-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"},{"identifier":"privacy_policy","version":1,"timestamp":"2018-01-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"}]
```

#### with limit and pagination parameters:

```console
$ curl https://consent.iubenda.com/legal_notices/privacy_policy?limit=20&starting_after=3 \
  -H "ApiKey: your-private-api-key" \
  -G
```

##### response:

```json
[{"identifier":"privacy_policy","version":2,"timestamp":"2018-03-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"},{"identifier":"privacy_policy","version":1,"timestamp":"2018-01-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"}]
```
