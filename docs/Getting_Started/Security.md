# Storing Database Passwords
The Delphix Masking Engine uses encryption and stores all passwords encrypted in
the application's repository database.

# Authenticating Users
If you choose to use the Delphix Masking Engine internal authentication, the
engine uses encryption and stores passwords for each user encrypted in the
engine relational repository.

When a user logs in to the Delphix Masking Engine and enters their username and
password, the engine verifies that the user is an active user with the Delphix
Masking Engine, and then authenticates their password.

Optionally, the Delphix Masking Engine can integrate with external
authentication software (Microsoft Active Directory, CA SiteMinder, or LDAP) to
authenticate users. If you integrate with external authentication software, the
Delphix Masking Engine will validate that the user has rights to access the
application and will login the user automatically. (No additional Delphix
Masking Engine password will be required.)

# Authorizing Users (Roles)
With the built-in Delphix Masking Engine Administrator role, which is similar to
a superuser role, the administrator can add roles and assign the roles to users. 
By creating specific roles and assigning them, the administrator can control
which users are authorized to perform various tasks (privileges).
