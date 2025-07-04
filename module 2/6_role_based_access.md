# Role Based Access Control (RBAC)
Snowflake uses role based access control to provide access to different assets to a user. It makes the management of privilege to a user flexible and simple. You can create a role that will have access to privileges. You can then assign that role to a user.

## System Defined Roles
Below are the list of roles defined by snowflake by default. There are very powerful roles.
1. orgadmin
1. accountadmin
1. sysadmin
1. securityadmin
1. useradmin
1. public

Below queries can be used to create, grant and manage role.

```SQL
USE ROLE accountadmin;

---> create a role
CREATE ROLE tasty_de;

---> see what privileges this new role has
SHOW GRANTS TO ROLE tasty_de;

---> see what privileges an auto-generated role has
SHOW GRANTS TO ROLE accountadmin;

---> grant a role to a specific user
GRANT ROLE tasty_de TO USER [username];

---> use a role
USE ROLE tasty_de;

---> try creating a warehouse with this new role
CREATE WAREHOUSE tasty_de_test;

USE ROLE accountadmin;

---> grant the create warehouse privilege to the tasty_de role
GRANT CREATE WAREHOUSE ON ACCOUNT TO ROLE tasty_de;

---> show all of the privileges the tasty_de role has
SHOW GRANTS TO ROLE tasty_de;

USE ROLE tasty_de;

---> test to see whether tasty_de can create a warehouse
CREATE WAREHOUSE tasty_de_test;

---> learn more about the privileges each of the following auto-generated roles has

SHOW GRANTS TO ROLE securityadmin;

SHOW GRANTS TO ROLE useradmin;

SHOW GRANTS TO ROLE sysadmin;

SHOW GRANTS TO ROLE public;
```