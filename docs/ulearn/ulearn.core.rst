===========
ulearn.core
===========

Community creation
------------------

There are a role for each community type:
 * "CC open"
 * "CC closed"
 * "CC organizative"

The users or groups with permissions to create each community type should be
granted the corresponding global role. The "WebMaster" role retains all the
grants to create all type of communities.

..note::

    At the time of writing, this feature only works with global roles.


Sync LDAP attributes with Plone user properties using PAS
---------------------------------------------------------

First, we need to be able to bind to the LDAP server with an user with enough
permissions to perform the changes in the desired LDAP attributes. Then, we need
to setup accordingly the LDAP server parameters in acl_users using the LDAP
Plugin.

After this, the "Properties Plugins" should be enabled for this LDAP connection
and the connection should have maximum preference (at the top) of the
"Properties Plugins".

The properties with read/write access should exist for Plone by extending the
user properties the standard Plone way using the p.a.users extender utility and
creating them in the portal_memberdata as needed.

The read only properties should live in the portal_memberdata.

For every property that we want to be user updatable it should be mapped to the
related LDAP attribute by using the acl_users/content/acl_users/LDAP Schema.
