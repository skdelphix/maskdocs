# Security

## Storing Database Passwords
The Delphix Masking Engine uses encryption and stores all passwords encrypted in
the application's repository database.

## User Authentication

When a user logs in to the Delphix Masking Engine and enters their username and
password, the engine verifies that the user is an active user with the Delphix
Masking Engine, and then authenticates their password. The application may be configured to authenticate passwords using either:

* Local authentication: A user's password is validated using information stored in the appliction's repository database. Following password management best practices, the user's actual password is not stored in application's repository.

* Active Directory/LDAP Authentication: A user's password is validated by consulting Active Directory/LDAP.

## User Authorization (Roles)
With the built-in Delphix Masking Engine Administrator role, which is similar to
a superuser role, the administrator can add roles and assign the roles to users. 
By creating specific roles and assigning them, the administrator can control
which users are authorized to perform various tasks (privileges).

