# Create/Upgrade a Database

If this is your first install, create a database with:
  initdb /usr/local/var/postgres

To migrate existing data from a previous major version (pre-9.1) of PostgreSQL, see:
  http://www.postgresql.org/docs/9.1/static/upgrading.html

# Start/Stop PostgreSQL

If this is your first install, automatically load on login with:
  mkdir -p ~/Library/LaunchAgents
  cp /usr/local/Cellar/postgresql/9.1.2/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents/
  launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist

If this is an upgrade and you already have the homebrew.mxcl.postgresql.plist loaded:
  launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
  cp /usr/local/Cellar/postgresql/9.1.2/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents/
  launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist

Or start manually with:
  PGA\q

And stop with:
  pg_ctl -D /usr/local/var/postgres stop -s -m fast

# Loading Extensions

By default, Homebrew builds all available Contrib extensions.  To see a list of all
available extensions, from the psql command line, run:
  SELECT * FROM pg_available_extensions;

To load any of the extension names, navigate to the desired database and run:
  CREATE EXTENSION [extension name];

For instance, to load the tablefunc extension in the current database, run:
  CREATE EXTENSION tablefunc;

For more information on the CREATE EXTENSION command, see:
  http://www.postgresql.org/docs/9.1/static/sql-createextension.html
For more information on extensions, see:
  http://www.postgresql.org/docs/9.1/static/contrib.html

# Other

Some machines may require provisioning of shared memory:
  http://www.postgresql.org/docs/current/static/kernel-resources.html#SYSVIPC

To install postgresql ( and ossp-uuid ) in 32 bits mode; you may use --32-bit :
   brew install postgresql --32-bit

If you want to install the postgres gem, including ARCHFLAGS is recommended:
    env ARCHFLAGS="-arch x86_64" gem install pg

To install gems without sudo, see the Homebrew wiki.