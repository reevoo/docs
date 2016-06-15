# API

We've decided to follow the [Heroku API Guideline](https://github.com/interagent/http-api-design) as a good starting point for all our new APIs.

## Security

We expect all access to our APIs to be over https.

## Exceptions and clarifications

### API versioning

We include the API version into URL in format `http[s]://$server/api/v$api_version_number/$resource_and_actions`

Example: `https://client-portal.reevoo.com/api/v1/clients/e978b3ef-a43d-41b1-b72c-05e129f162ca`


### Pagination by ranges

For pagination of resources we utilize the HTTP headers `Range`, `Accept-Ranges` and `Content-Range`.

#### Request

The request of paginated resource can include header `Range` with value consisting of resource name in plural form and
index of first and last record in format `$resource_name=$index_of_first_record-$index_of_last_record` Records are indexed from 0.

Example: `Range: clients=0-19`

The whole header can be omitted, in such case the default range of records should be returned.


#### Response

The response code is *206 Partial Content* unless whole list of records is returned.

Every HTTP response with paginated resource include headers `Accept-Ranges` and `Content-Range`.
Value of `Accept-Ranges` is a resource name in plural form.
(According the RFC 2616 you can specify multiple resources separated by comma, but in case of our resource oriented architecture
every API endpoint deals with a single resource.)

Example: `Accept-Ranges: clients`

Value of `Content-Range` consists from resource name in plural form, index of the first and last record and count of all records in format
`
$resource_name $index_of_first_record-$index_of_last_record/$count_of_all_records`. Records are indexed from 0.

Example: `Content-Range: clients 0-19/53`

Count of all records can be omitted if such operation is not efficient. In such case the number is replaced by `*` (example `Content-Range: clients 20-29/*`)

### Accepting Extra Data

Unless there is a good reason not to, we accept and ignore any JSON data that is sent, but not required by an API endpoint. For example, if an endpoint accepts attributes `id` and `timestamp`, and the request is `{ id: 1, timestamp: '2014-01-01 00:00:00', password: 'new' }`, the request will be accepted but `password` will be ignored.

We could have raised an error for a packet with extra data, to give clients a hint that their data will not be accepted. This choice is to ease deployments: the client can be updated to send new parameters *and then* the server can be updated to accept it.

## Resources

- https://devcenter.heroku.com/articles/platform-api-reference
- HTTP Range: http://otac0n.com/blog/2012/11/21/range-header-i-choose-you.html
