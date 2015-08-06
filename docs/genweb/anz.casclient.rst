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

