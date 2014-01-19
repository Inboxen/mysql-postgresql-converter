MySQL to PostgreSQL Converter
=============================

Forked from Lanyrd's MySQL to PostgreSQL conversion script. Use with care.

This script was changed for our specific database and column requirements -
notably, VARCHARs have COLLATE removed beacuse we used utf8mb4 in MySQL (which
Postgres calls utf8), places indexes on all foreign keys, and presumes you're
using Django for column typing purposes.

To reiterate: this script assumes your MySQL database was using the utf8mb4
encoding and the target Postgres database is using utf8.

How to use
----------

First, dump your MySQL database in PostgreSQL-compatible format

    mysqldump --compatible=postgresql --default-character-set=utf8 \
    -r databasename.mysql -u root databasename

Then, convert it using the dbconverter.py script

`python dbconverter.py databasename.mysql databasename.psql`

It'll print progress to the terminal.

Finally, load your new dump into a fresh PostgreSQL database using: 

`psql -f databasename.psql`

More information
----------------

You can learn more about the move which this powered at
<http://lanyrd.com/blog/2012/lanyrds-big-move/> and some technical details of it
at <http://www.aeracode.org/2012/11/13/one-change-not-enough/>. You can out
about Inboxen's motives at <https://inboxen.org/blog/post/12>.
