Tiny SAML IDP
======

Tiny SAML IDP a tiny SAML2 Identity Provider.
It is based on [Mujina](https://github.com/OpenConext/Mujina).

The IdP will authenticate known users, providing known attributes to any SP (SAML service provider).

Defaults
--------
The default Identity Provider configuration is as follows:

* The Entity ID is "http://mock-idp"
* It has a user with login "admin" and password "secret" with roles ROLE_USER and ROLE_ADMIN
* It has a user with login "user" and password "secret" with role ROLE_USER
* It has the following attributes. Attributes are always stored as lists. Even when they contain a single value.
    * "urn:mace:dir:attribute-def:uid" is "john.doe"
    * "urn:mace:dir:attribute-def:cn" is "John Doe"
    * "urn:mace:dir:attribute-def:givenName" is "John"
    * "urn:mace:dir:attribute-def:sn" is "Doe"
    * "urn:mace:dir:attribute-def:displayName" is "John Doe"
    * "urn:mace:dir:attribute-def:mail" is "j.doe@example.com"
    * "urn:mace:terena.org:attribute-def:schacHomeOrganization" is "example.com"
    * "urn:mace:dir:attribute-def:eduPersonPrincipalName" is "j.doe@example.com"
    * "urn:oid:1.3.6.1.4.1.1076.20.100.10.10.1" is "guest"
* There is a default certificate and private key available
* By default the ACS endpoint should be provided by the SP as an attribute in the AuthnRequest.

Build
---------------

[Maven 3](http://maven.apache.org) is needed to build and run.

The build dependencies are hosted on https://build.surfconext.nl/repository/public/
(and will be fetched automatically by Maven).

Run the IDP using jetty
-----------------------

```bash
mvn clean install
cd mujina-idp
mvn jetty:run
```

Then, go to https://localhost:8443/ or http://localhost:8080/

Changing port numbers
----------------------
It can be made to bind to a different tcp/ip port: 
`mvn jetty:run -DhttpPort=8082 -DhttpsPort=8444`
