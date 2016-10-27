<pre>___  ___        _  _
|  \/  |       (_)(_)
| .  . | _   _  _  _  _ __    __ _
| |\/| || | | || || || '_ \  / _` |
| |  | || |_| || || || | | || (_| |
\_|  |_/ \__,_|| ||_||_| |_| \__,_|
              _/ |
             |__/

  Mock Identity and Service Provider using OpenSAML
</pre>

Mujina
======

Mujina mocks a SAML2 Identity and Service Provider (IdP & SP).
Almost all characteristics of either the IdP or SP can be configured on-the-fly using a REST API. This approach removes the need for special test configuration sets in your set-up.
Thus, Mujina makes testing your stack a breeze! Mujina can be used in combination with test suites like Selenium or Jmeter to automate authentication testing for your applications.

Mujina is used to test the SURFconext middleware which enables Dutch educational services to use cloud based SAAS-services.
SURFconext also exposes a REST API for  Service Providers to offer the end-user context about the groups and memberships of the user (typically students, researchers and educational advisors).
Mujina SP and IdP can be used to test the SURFconext cloud broker capabilities.
The OAuth playground - part of the REST API component - can be used to test the SURFconext REST API (or any other OAuth compliant API like Google, Twitter, Facebook or Foursquare).

Features
--------
- A SAML2 complient Identity Provider. The IdP will authenticate known users, providing known attributes to the SP.

- A SAML2 complient Service Provider. The SP displays the attributes as these were received from an IdP.

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

The default Service Provider configuration is as follows:

* The Entity ID is "http://mock-sp"
* There is a default certificate and private key available

In this document you will find some examples for overriding the default configuration.
After you override configuration you can go back to the default using the reset API.

Build Mujina
---------------

[Maven 3](http://maven.apache.org) is needed to build and run Mujina.

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

Run the SP using jetty
----------------------

```bash
mvn clean install
cd mujina-sp
mvn jetty:run
```

Then, go to http://localhost:9090/. You will be redirected to the IdP, where you can
login with username admin and password secret.

Changing port numbers
----------------------
Both the SP and IDP can be made to bind to a different tcp/ip port: 
`mvn jetty:run -DhttpPort=8082 -DhttpsPort=8444`
