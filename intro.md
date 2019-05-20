# Intro
The OldMusa project defines a series of utilities that help managing sites.
It's original purpose was to manage sensors located into museums, further in
the development process that was generified to sites, allowing non-museum
structures to fall into this same category (that's why you can see museum
instead of site in our older codebase).
At the time of writing there is only a server and an android client.
In order for the server and the client to communicate there is a REST contract
that describes what an application can do.

## Communication
The android client for now communicates trought normal rest queries
(via HTTP1.1), there were plans to implement a connection-oriented
websocket-based communication so that the server could send realtime data to the
application but for now the support is missing in both the server and the
client. In the event of a future implementation the rest protocol that the
app relies on will remain unchanged, as the developer shouldn't see any
differences between the two connection types.

## Authentication
The original app was tought to use an HTTPS connection to encrypt every single
query to the server, as this is still not implemented the server has a basic
token system. The client should first ask the user to login, then using the
login information the client obtains a token that can safely store on some
traditional storing method (an eventual hacker has no chance of getting the
user password from the token). The token should remain valid until the user
password is changed and it does not have any time contraint.
It should be said that this method is still NOT SECURE until an HTTPS connection
is implemented as an eventual attaccker could steal the token and act the way
of a normal user even without knowing his password.

## Request Arguments
Some of the queries require arguments that are not specified in the url path.
Those can be provided both in the query request parameters and in the body
(json-encoded), unless the body is already used for other purposes.<br>
Ex: obtaining a token:<br>
arguments: username and password<br>
```curl -X GET ${API_URL}/token?username=root&password=password```
