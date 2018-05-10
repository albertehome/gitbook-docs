# dropuser

dropuser — remove a PostgreSQL user account

### Synopsis

`dropuser` \[_`connection-option`_...\] \[_`option`_...\] \[_`username`_\]

### Description

dropuser removes an existing PostgreSQL user. Only superusers and users with the `CREATEROLE` privilege can remove PostgreSQL users. \(To remove a superuser, you must yourself be a superuser.\)

dropuser is a wrapper around the SQL command [DROP ROLE](https://www.postgresql.org/docs/10/static/sql-droprole.html). There is no effective difference between dropping users via this utility and via other methods for accessing the server.

### Options

dropuser accepts the following command-line arguments:

_`username`_

Specifies the name of the PostgreSQL user to be removed. You will be prompted for a name if none is specified on the command line and the `-i`/`--interactive` option is used.

`-e`  
`--echo`

Echo the commands that dropuser generates and sends to the server.

`-i`  
`--interactive`

Prompt for confirmation before actually removing the user, and prompt for the user name if none is specified on the command line.

`-V`  
`--version`

Print the dropuser version and exit.

`--if-exists`

Do not throw an error if the user does not exist. A notice is issued in this case.

`-?`  
`--help`

Show help about dropuser command line arguments, and exit.

dropuser also accepts the following command-line arguments for connection parameters:

`-h `_`host`_  
`--host=`_`host`_

Specifies the host name of the machine on which the server is running. If the value begins with a slash, it is used as the directory for the Unix domain socket.

`-p `_`port`_  
`--port=`_`port`_

Specifies the TCP port or local Unix domain socket file extension on which the server is listening for connections.

`-U `_`username`_  
`--username=`_`username`_

User name to connect as \(not the user name to drop\).

`-w`  
`--no-password`

Never issue a password prompt. If the server requires password authentication and a password is not available by other means such as a `.pgpass` file, the connection attempt will fail. This option can be useful in batch jobs and scripts where no user is present to enter a password.

`-W`  
`--password`

Force dropuser to prompt for a password before connecting to a database.

This option is never essential, since dropuser will automatically prompt for a password if the server demands password authentication. However, dropuser will waste a connection attempt finding out that the server wants a password. In some cases it is worth typing `-W`to avoid the extra connection attempt.

### Environment

`PGHOST`  
`PGPORT`  
`PGUSER`

Default connection parameters

This utility, like most other PostgreSQL utilities, also uses the environment variables supported by libpq \(see [Section 33.14](https://www.postgresql.org/docs/10/static/libpq-envars.html)\).

### Diagnostics

In case of difficulty, see [DROP ROLE](https://www.postgresql.org/docs/10/static/sql-droprole.html) and [psql](https://www.postgresql.org/docs/10/static/app-psql.html) for discussions of potential problems and error messages. The database server must be running at the targeted host. Also, any default connection settings and environment variables used by the libpq front-end library will apply.

### Examples

To remove user `joe` from the default database server:

```text
$ dropuser joe
```

To remove user `joe` using the server on host `eden`, port 5000, with verification and a peek at the underlying command:

```text
$ dropuser -p 5000 -h eden -i -e joe
Role "joe" will be permanently removed.
Are you sure? (y/n) y
DROP ROLE joe;
```

### See Also

[createuser](createuser.md), [DROP ROLE](../sql-commands/drop-role.md)
