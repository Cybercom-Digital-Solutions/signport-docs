# Documents

All creation and management of documents can be done using the following endpoints

## Get all documents

```shell
curl "http://signport.com/api/documentservice/v1/documents"
  -H "Authorization: <ACCESS_TOKEN>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "ID":25,
    "CreatedAt":"2017-06-28T19:08:22.098555Z",
    "UpdatedAt":"2017-06-28T19:08:22.098555Z",
    "Author":"190102030400",
    "Permissions":"YourCompany",
    "DocumentURL":"/documentstorage/2017-06-28T19:08:22.006555464Z-document_to_sign.pdf",
    "Signers":[
      {
        "ID":25,
        "FirstName":"Lisa",
        "LastName":"Svensson",
        "Email":"lisa@test.se",
        "Ssn":"190102030401",
        "Signed":true
      }
    ],
    "ReturnURL":"https://www.yourcompany.se/finishedsigning",
    "SigningOrder": false
  },
  {
    "ID":26,"CreatedAt":"2017-06-28T19:16:08.023052Z",
    "UpdatedAt":"2017-06-28T19:16:08.023052Z",
    "DeletedAt":null,
    "Author":"190102030400",
    "Permissions":"YourCompany",
    "DocumentURL":"/documentstorage/2017-06-28T19:16:07.95853269Z-another_document_to_sign",
    "Signers":[
      {
        "ID":26,
        "FirstName":"Sven",
        "LastName":"Svensson",
        "Email":"sven@test.se",
        "Ssn":"190102030402",
        "Signed":false
      }
    ],
    "ReturnURL":"https://www.yourcompany.se/finishedsigning",
    "SigningOrder": false
  },
  ...
]
```

This endpoint retrieves all documents.

### HTTP Request

`GET http://signport.com/api/documentservice/v1/documents`


## Get a specific document

```shell
curl "http://signport.com/api/documentservice/v1/documents/25"
  -H "Authorization: <ACCESS_TOKEN>"
```

> The above command returns JSON structured like this:

```json
{
  "ID":25,
  "CreatedAt":"2017-06-28T19:08:22.098555Z",
  "UpdatedAt":"2017-06-28T19:08:22.098555Z",
  "Author":"190102030400",
  "Permissions":"YourCompany",
  "DocumentURL":"/documentstorage/2017-06-28T19:08:22.006555464Z-document_to_sign.pdf",
  "Signers":[
    {
      "ID":25,
      "FirstName":"Lisa",
      "LastName":"Svensson",
      "Email":"lisa@test.se",
      "Ssn":"190102030401",
      "Signed":true
    }
  ],
    "ReturnURL":"https://www.yourcompany.se/finishedsigning",
    "SigningOrder": false
}
```

This endpoint retrieves a specific document.

### HTTP Request

`GET http://signport.com/api/documentservice/v1/documents/<ID>`

### Url Parameters

Parameter | Description
--------- | -----------
ID | The ID of the document to retrieve

## Create a new document

```shell
curl "http://signport.com/api/documentservice/v1/documents/25"
  -X POST
  -H "Authorization: <ACCESS_TOKEN>"
  -F "authorSsn=190102030400"
  -F "signers=[{'Ssn':'190102030401'}]"
  -F "permissions=yourCompany"
  -F "document=@/path/document_to_sign.pdf"
  -F "signingOrder=false"
```

> The above command returns JSON structured like this:

```json
{
  "Document": {
    "ID":25,
    "CreatedAt":"2017-06-28T19:08:22.098555Z",
    "UpdatedAt":"2017-06-28T19:08:22.098555Z",
    "Author":"190102030400",
    "Permissions":"yourCompany",
    "DocumentURL":"/documentstorage/2017-06-28T19:08:22.006555464Z-document_to_sign.pdf",
    "Signers":[
      {
        "ID":25,
        "Ssn":"190102030401",
        "Signed":false
      }
    ],
    "ReturnURL":"",
    "SigningOrder": false,
    "State":""
  },
  "SigningURL": "http://signport.com/api/documentservice/v1/sign/25"
}
```

This endpoint handles uploads of new documents to sign

### HTTP Request

`POST http://signport.com/api/documentservice/v1/documents`

### Form Parameters

Parameter | Default | Description
--------- | ----- | -----------
authorSsn || Ssn of author, if not set the author will be owner of <ACCESS_TOKEN>
signers || JSON array of signers, A signer could include: Firstname, Lastname, Email, Phone, Ssn
permissons | The group of your token | The group with access to read document
document || The document to be signed
signingOrder| false | A true or false vaule. If set to true, users will be able to sign in the order of signers. Mail will be sent to the signer who's next in turn if sendEmail is true.
returnurl? | empty | If you want the user to be sent to a specific URL after signing, this is where you'd put it
sendEmail? | false | A true or false value. If set to true, the user will be sent an email invitation to sign the document. (Requires email set in signer)
state? | empty | The state parameter is used to preserve some state object from the requesting service

## Update a specific document

This endpoint handles updates of a specific document

### HTTP Request

`PUT http://signport.com/api/documentservice/v1/documents/<ID>`

### Url Parameters

Parameter | Description
--------- | -----------
ID | Which document to update

### Form Parameters

Same parameters as the request to create a new document.

Parameter | Description
--------- | -----------
...| Form parameters in POST request above

## Delete a specific document

```shell
curl "http://signport.com/api/documentservice/v1/documents/25"
  -X DELETE
  -H "Authorization: <ACCESS_TOKEN>"
```

This endpoint handles the deletion of a specific document

### HTTP Request

`DELETE http://signport.com/api/documentservice/v1/documents/<ID>`

### Url Parameters

Parameter | Description
--------- | -----------
ID | Which document to delete

# Signers

The signers endpoint handles retrieving and updating of signers for documents

## Get all signers

```shell
curl "http://signport.com/api/documentservice/v1/signers"
  -X POST
  -H "Authorization: <ACCESS_TOKEN>"
```

> The above command returns JSON structured like this:

```json
[
	{
		"ID": 32,
		"CreatedAt": "2017-08-09T11:23:12.813551Z",
		"UpdatedAt": "2017-08-09T11:23:12.813551Z",
		"DocumentID": 37,
		"FirstName": "Sven",
		"LastName": "Svensson",
		"Email": "sven@test.se",
		"Phone": "123456",
		"Ssn": "190102030400",
		"Signed": false
	},
	{
		"ID": 37,
		"CreatedAt": "2017-08-09T11:23:12.813551Z",
		"UpdatedAt": "2017-08-09T11:23:12.813551Z",
		"DocumentID": 37,
		"FirstName": "Lena",
		"LastName": "Svensson",
		"Email": "lena@test.se",
		"Phone": "123456",
		"Ssn": "199212140538",
		"Signed": false
	},
  ...
]
```

This endpoint retrieves all signers

### HTTP Request

`GET http://signport.com/api/documentservice/v1/signers`

## Update a specific signer

This endpoint can update an already existing signer, e.g. to add new information

### HTTP Request

`PUT http://signport.com/api/documentservice/v1/signers/<ID>`

### Url Parameters

Parameter | Description
--------- | -----------
ID | The ID of the signer to update

### Url Parameters

Parameter | Description
--------- | -----------
Firstname | The firstname of signer
Lastname  | The lastname of signer
Email     | The email of signer
Phone     | The phone of signer

# Signing

The following endpoints is used for signing

## Initiate signing

```shell
curl "http://signport.com/api/documentservice/v1/signrequest/<ID>"
  -X POST
  -H "Authorization: <ACCESS_TOKEN>"
```

> The above command returns JSON structured like this:

```json
{
	"Success": true,
	"Binding": "POST/XML/1.0",
	"RelayState": "928ae68c-e37f-4737-879b-2d95661201a0",
	"EidSignRequest": "PFNpZ25SZXF1ZXN0IHhtbG5zOnhzZD0iaHR0cDovL3d3dy53My5vcmcvMjAwMS9YTUxTY2hlbWEi.....",
	"SigningServiceURL": "https://eid.identityhub.se/demo/ut/sign/BeginSigning"
}
```

This endpoint creates a signing-request that should be sent to our IDP.

If `"Success": true` you are free to submit Binding, RelayState and EidSignRequest as a form to the `SigningServiceUrl`.

### HTTP Request

`POST http://signport.com/api/documentservice/v1/signrequest/<ID>`

### Url Parameters

Parameter | Description
--------- | -----------
ID | The ID of the document to sign

# Files

## Get a specific file

To get the raw unsigned/signed file use this endpoint

### HTTP Request

`PUT http://signport.com/api/documentservice/v1/file/<FILEPATH>`

### Url Parameters

Parameter | Description
--------- | -----------
FILEPATH | The filepath that points to the requested document. Received when creating document and from /documents endpoint
