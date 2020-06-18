### `POST /beta/consent`

```php
$consent_data = array(
    "subject" => array(
        "id" => "J02eZvKYlo2ClwuJ1",
        "email" => "subject@example.com"
    ),
    "legal_notices" => array(
        array(
            "identifier" => "newsletter"
        ),
        array(
            "identifier" => "privacy_policy"
        )
    ),
    "proofs" => array(
        array(
            "content" => "proof_content",
            "form" => "proof_form"
        )
    ),
    "preferences" => array(
        "newsletter" => true,
        "privacy_policy" => true
    ),
    "ip_address" => "127.0.0.1",
    "consent_type" => null
);

$req = curl_init();
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/consent');
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));
curl_setopt($req, CURLOPT_POST, true);
curl_setopt($req, CURLOPT_POSTFIELDS, json_encode($consent_data));

$response = curl_exec($req);
```

##### response:

```json
{"id":"7abe5f70-22e4-4181-878c-9f931034fab5","timestamp":"2018-06-08T08:25:30.395Z","subject_id":"J02eZvKYlo2ClwuJ1"}
```

### `GET /beta/consent`

```php
$req = curl_init();
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/consent');
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));

$response = curl_exec($req);
```

##### response:

```json
[{"id":"b04c4b2b-80b7-439f-8997-ade3d35cbb95","timestamp":"2018-06-04T08:11:34.000+00:00","owner":"12345","source":"private","subject":{"id":"0e371678-634a-4016-83ce-9b7c36f828e6","email":"83ce_634a_4016_9b7c36f828e6_0e371678@example.com","first_name":"Kianna","last_name":"Fahey","full_name":"Kianna Fahey","verified":false},"consent_type":"cookie_policy","preferences":{"newsletter":false},"ip_address":"79.42.49.139"},{"id":"ee6644ea-08e9-4aaa-a7a9-18602731a123","timestamp":"2018-06-04T08:11:33.000+00:00","owner":"12345","source":"public","subject":{"id":"8c6d1b71-0908-4604-948f-2f706500b5b1","email":"0908.8c6d1b71.2f706500b5b1.4604.948f@example.org","first_name":"Eleanora","last_name":"Adams","full_name":"Eleanora Adams","verified":false},"consent_type":null,"preferences":{"newsletter":true},"ip_address":null},{"id":"bf12770e-840a-40cd-ab79-5d88576b6b73","timestamp":"2018-06-04T08:11:33.000+00:00","owner":"12345","source":"public","subject":{"id":"d4f24d92-56c2-4372-8696-fec829da5ccc","email":"fec829da5ccc.8696.4372.56c2.d4f24d92@example.com","first_name":"Hank","last_name":"Klein","full_name":"Hank Klein","verified":false},"consent_type":null,"preferences":{"newsletter":false},"ip_address":"79.42.49.139"}]
```

### `GET /beta/consent/:id`

```php
$req = curl_init();
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/consent/7abe5f70-22e4-4181-878c-9f931034fab5');
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));

$response = curl_exec($req);
```

##### response:

```json
{"id":"1dbbc6f8-6a57-4407-b687-d6e6f818742f","timestamp":"2018-05-04T14:52:26Z","owner":"1","subject":{"id":"custom_subject_id","owner_id":"1","email":"subject@example.com","first_name":"John","last_name":"Doe","verified":false},"preferences":{"privacy_policy":true,"newsletter":false},"legal_notices":[{"identifier":"privacy_policy","version":123},{"identifier":"terms_and_conditions","version":123}],"proofs":[{"content":"proof_1","form":"proof_1 form"},{"content":"proof_2","form":"proof_2 form"}],"ip_address":null,"consent_type":null}
```

### `GET /beta/subjects`

```php
$subject_data = array(
    "email" => "subject@example.com",
    "first_name" => "John",
    "last_name" => "Doe"
);

$req = curl_init();
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/subjects');
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));
curl_setopt($req, CURLOPT_POST, true);
curl_setopt($req, CURLOPT_POSTFIELDS, json_encode($subject_data));

$response = curl_exec($req);
```

##### response:

```json
[{"id":"d2a55da5-0777-4625-94bd-b69948703e71","owner_id":"131132","email":"rath.jorge@example.com","first_name":"Jorge","last_name":"Rath","full_name":"Jorge Rath","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"b75c6d0c-550f-4f84-9e92-2f351d481220","owner_id":"131132","email":"aufderhar_alfonso@example.net","first_name":"Alfonso","last_name":"Aufderhar","full_name":"Alfonso Aufderhar","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"a9c8c720-cb07-4a52-81c3-7cb7fb4f877e","owner_id":"131132","email":"vandervort.furman@example.net","first_name":"Furman","last_name":"Vandervort","full_name":"Furman Vandervort","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"6ccc2802-3bcb-49af-a4c5-14dc89ba94bc","owner_id":"131132","email":"alvis.rohan@example.org","first_name":"Alvis","last_name":"Rohan","full_name":"Alvis Rohan","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"},{"id":"5900f856-619e-42b0-92a5-b2ebd016ac01","owner_id":"131132","email":"brown.marlee@example.net","first_name":"Marlee","last_name":"Brown","full_name":"Marlee Brown","preferences":null,"verified":true,"timestamp":"2018-09-12T16:22:21+00:00"}]
```

### `POST /beta/subjects`

```php
$subject_data = array(
    "email" => "subject@example.com",
    "first_name" => "John",
    "last_name" => "Doe"
);

$req = curl_init();
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/subjects');
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));
curl_setopt($req, CURLOPT_POST, true);
curl_setopt($req, CURLOPT_POSTFIELDS, json_encode($subject_data));

$response = curl_exec($req);
```

##### response:

```json
{"id":"df39c1bf-5f27-4c3a-bf94-64360cc7e4f8","timestamp":"2018-06-11T08:57:13.662Z"}
```

### `GET /beta/subjects/:id`

```php
$req = curl_init();
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/subjects/df39c1bf-5f27-4c3a-bf94-64360cc7e4f8');
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));

$response = curl_exec($req);
```

```json
{"id":"9f5a50f6-052c-4595-8bc4-760dc05d86ba","owner_id":"123","email":"john@example.com","first_name":"John","last_name":"Doe","full_name":null,"preferences":null,"verified":false,"timestamp":"2018-06-06T11:05:41+00:00"}
```

### `PATCH /beta/subjects/:id`

```php
$subject_data = array(
    "first_name" => "Mary"
);

$req = curl_init();
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/subjects/df39c1bf-5f27-4c3a-bf94-64360cc7e4f8');
curl_setopt($curl, CURLOPT_CUSTOMREQUEST, 'PATCH');
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));
curl_setopt($req, CURLOPT_POSTFIELDS, json_encode($subject_data));

$response = curl_exec($req);
```

##### response:

```json
{"id":"df39c1bf-5f27-4c3a-bf94-64360cc7e4f8","timestamp":"2018-06-11T08:57:13.000+00:00"}
```

### `POST /beta/legal_notices`

```php
$legal_notice_data = array(
    "identifier" => "privacy_policy",
    "content" => "privacy policy legal text"
);

$req = curl_init();
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/legal_notices');
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));
curl_setopt($req, CURLOPT_POST, true);
curl_setopt($req, CURLOPT_POSTFIELDS, json_encode($legal_notice_data));

$response = curl_exec($req);
```

##### response:

```json
{"identifier":"privacy_policy","version":1,"timestamp":"2018-06-11T10:26:00.413Z"}
```

### `GET /beta/legal_notices`

```php
$legal_notice_data = array(
    "identifier" => "privacy_policy",
    "content" => "privacy policy legal text"
);

$req = curl_init();
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/legal_notices');
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));
curl_setopt($req, CURLOPT_POST, true);
curl_setopt($req, CURLOPT_POSTFIELDS, json_encode($legal_notice_data));

$response = curl_exec($req);
```

##### response:

```json
[{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":20,"timestamp":"2018-10-09T12:38:04Z","content":{"en":"Et vinculum clam decerno arguo admoveo velum sponte tot suppellex venustas defendo dolor decumbo est.","it":"Collum tutis esse confugo porro urbs varius abscido turpis decor praesentium tardus voluptate fugit numquam."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":19,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Venia valde vel surculus capitulus adfectus patior comparo acsi cur vero super cursim.","it":"Consuasor arcesso conscendo crudelis cauda aer aut adeptio illo argentum comis subiungo subito colo."}},{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":18,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Ullus voco aufero speculum fugiat audacia laboriosam vilicus amita trans aut ut.","it":"Alo veritatis ipsa tristis cuius occaecati adflicto creta verecundia facere solvo despirmatio cupiditate crinis aqua bos."}},{"id":"0_privacy_policy","owner_id":"0","identifier":"privacy_policy","version":17,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Confero succedo caelum adhaero quo vir deorsum quaerat utor sit ustulo cribro.","it":"Bibo cubitum unus est ambitus contego apparatus alo via abutor utroque xiphias voco."}},{"id":"0_privacy_policy","owner_id":"0","identifier":"privacy_policy","version":16,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Qui porro culpo attero benevolentia aut sed sulum adfero artificiose adsidue tam amo validus vel spectaculum.","it":"Cerno ipsum fugit compello cursim ter surgo asporto debilito excepturi adversus facere."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":15,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Tunc timidus veritatis maiores advenio aperio testimonium defluo celo cuius adsuesco deripio.","it":"Depulso dignissimos vinitor curatio caelestis cedo et sum concedo id admoneo appositus."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":14,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Repellat mollitia desidero videlicet est textilis stips nisi aequus solum depromo agnitio usus.","it":"Vomito tonsor comitatus illum aut usitas laboriosam canonicus tepesco benigne confugo trado."}},{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":13,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Temperantia alias somniculosus absorbeo utique caecus terror demitto trucido desidero baiulus sublime.","it":"Perspiciatis at tredecim curriculum comprehendo deduco corrupti attonbitus barba cruentus communis comparo thorax cauda spero vito anser."}},{"id":"0_cookie_policy","owner_id":"0","identifier":"cookie_policy","version":12,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Allatus cena surculus ventito ver adversus torrens demo venustas toties veritas qui cado vis.","it":"Talio avoco aptus compono et subiungo peior bellum depromo aureus torqueo adeptio nobis."}},{"id":"0_terms","owner_id":"0","identifier":"terms","version":11,"timestamp":"2018-10-09T12:38:03Z","content":{"en":"Aliquam cubicularis tergum utor cinis concido ratione vociferor uter deduco tertius verecundia alo claustrum sto vos aegrotatio.","it":"Corona ut comes sub coaegresco caute casus laboriosam tremo vulariter aegrotatio pauci callide assentator basium."}}]
```


### `GET /beta/legal_notices/:identifier/:version`

```php
$req = curl_init();
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/legal_notices/privacy_policy/1');
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));

$response = curl_exec($req);
```

##### response:

```json
{"identifier":"privacy_policy","version":1,"timestamp":"2018-06-11T10:26:00.000+00:00","content":"privacy policy legal text"}
```

### `GET /beta/legal_notices/:identifier`

```php
$req = curl_init();
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/legal_notices/privacy_policy');
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));

$response = curl_exec($req);
```

##### response:

```json
[{"identifier":"privacy_policy","version":3,"timestamp":"2018-05-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"},{"identifier":"privacy_policy","version":2,"timestamp":"2018-03-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"},{"identifier":"privacy_policy","version":1,"timestamp":"2018-01-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"}]
```

#### with limit and pagination parameters:

```php
$req = curl_init();
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_URL, 'https://consent.iubenda.com/beta/legal_notices/privacy_policy?limit=3&starting_after=4');
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'ApiKey: your-secret-api-key',
    'Content-Type: application/json'
));

$response = curl_exec($req);
```

##### response:

```json
[{"identifier":"privacy_policy","version":2,"timestamp":"2018-03-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"},{"identifier":"privacy_policy","version":1,"timestamp":"2018-01-16T13:55:57Z","id":"1234_privacy_policy","owner_id":"1234","content":"privacy policy content"}]
```
