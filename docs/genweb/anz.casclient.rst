===================
anz.casclient
===================

This is the package that brings in the CAS PAS plugin. It allows a user to
authenticate via CAS protocol (in the UPC case, to the https://cas.upc.edu
service). For Genweb UPC it comes automatically configured to use it.

..note::

    In case that we want to use it with other CAS server, it should be
    configured as well to use that other server. See the companion package
    **upcnet.cas** for an example.

From version 1.1, the server is able to connect to a CAS server 3.x and above
and validate the service ticket (ST) against the CAS server using SAML, in order
to retrieve the extra fields for the authenticated user that the CAS server may
be providing. To use his feature, it's required to configure the plugin to use
the SAML validation by configuring the **SAMLValidate** property to ``True``.

..note::

    The **upcnet.cas** package is NOT currently configuring it by default, as
    this feature is not required in Genweb UPC yet. In case that we want it to
    use it in uLearn or other project, it is required to configure it
    programatically from the client/product package, and other diferent
    properties as well like the CAS server URL.


SAML service ticket validation
------------------------------

For documentation purposes, this is the response (with a valid ticket) received
from the CAS server in case we want to debug it::

    <?xml version="1.0" encoding="UTF-8"?>
      <SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
        <SOAP-ENV:Body>
          <saml1p:Response xmlns:saml1p="urn:oasis:names:tc:SAML:1.0:protocol" IssueInstant="2015-08-05T11:44:30.180Z" MajorVersion="1" MinorVersion="1" Recipient="http://127.0.0.1:8080/2/genwebupc/logged_in?came_from=http://127.0.0.1:8080/2/genwebupc/ca" ResponseID="_d198ccbe6b00a5f7dbbbaa309745dea1">
            <saml1p:Status>
              <saml1p:StatusCode Value="saml1p:Success" /></saml1p:Status>
            <saml1:Assertion xmlns:saml1="urn:oasis:names:tc:SAML:1.0:assertion" AssertionID="_56165254f06e8931aab6f5728aa9e5ea" IssueInstant="2015-08-05T11:44:30.180Z" Issuer="localhost" MajorVersion="1" MinorVersion="1">
              <saml1:Conditions NotBefore="2015-08-05T11:44:30.180Z" NotOnOrAfter="2015-08-05T11:45:00.180Z">
                <saml1:AudienceRestrictionCondition>
                  <saml1:Audience>http://127.0.0.1:8080/2/genwebupc/logged_in?came_from=http://127.0.0.1:8080/2/genwebupc/ca</saml1:Audience>
                </saml1:AudienceRestrictionCondition>
              </saml1:Conditions>
              <saml1:AuthenticationStatement AuthenticationInstant="2015-08-05T11:44:29.451Z" AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:password">
                <saml1:Subject>
                  <saml1:NameIdentifier>victor.fernandez</saml1:NameIdentifier>
                  <saml1:SubjectConfirmation>
                    <saml1:ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:artifact</saml1:ConfirmationMethod>
                  </saml1:SubjectConfirmation>
                </saml1:Subject>
              </saml1:AuthenticationStatement>
              <saml1:AttributeStatement>
                <saml1:Subject>
                  <saml1:NameIdentifier>user.name</saml1:NameIdentifier>
                  <saml1:SubjectConfirmation>
                    <saml1:ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:artifact</saml1:ConfirmationMethod>
                  </saml1:SubjectConfirmation>
                </saml1:Subject>
                <saml1:Attribute AttributeName="oauthToken" AttributeNamespace="http://www.ja-sig.org/products/cas/">
                  <saml1:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">fasdf8as7d768sadasd989asdas</saml1:AttributeValue>
                </saml1:Attribute>
                <saml1:Attribute AttributeName="idGauss" AttributeNamespace="http://www.ja-sig.org/products/cas/">
                  <saml1:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">1051861</saml1:AttributeValue>
                </saml1:Attribute>
              </saml1:AttributeStatement>
            </saml1:Assertion>
          </saml1p:Response>
        </SOAP-ENV:Body>
      </SOAP-ENV:Envelope>
