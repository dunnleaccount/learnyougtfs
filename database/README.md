The basics of putting GTFS into a database with the [OneBusAway GTFS Hibernate CLI](http://developer.onebusaway.org/modules/onebusaway-gtfs-modules/current/onebusaway-gtfs-hibernate-cli.html)

## Setup

1. Move into this directory `cd learnyougtfs/database`

2. Create a database called `gtfs` with the sql flavor of your choice.  If you're not familiar with or don't have a database software installed, the easiest to use is probably just HSQLDB (does not require setting up a separate database software). 

### Generic
```bash
java -classpath onebusaway-gtfs-hibernate-cli-1.3.3.jar:your-database-jdbc.jar \
 org.onebusaway.gtfs.GtfsDatabaseLoaderMain \
 --driverClass=... \
 --url=... \
 --username=... \
 --password=... \
 gtfs_path
```

### HSQLDB (default)
```bash
java -classpath onebusaway-gtfs-hibernate-cli-1.3.3.jar:hsqldb.jar \
 org.onebusaway.gtfs.GtfsDatabaseLoaderMain \
 --driverClass=org.hsqldb.jdbcDriver \
 --url=jdbc:hsqldb:file:gtfs \
 --username=user \
 --password=pass \
 ../data/google_transit.zip
```

Important! You will need to run the above command 2 times, the first time to create the tables and the second time is to insert the data. You can can copy and paste the texts.

After a successful gtfs import, run `java -jar sqltool.jar` to open the sql tools command line interface.

To connect to the `gtfs` database in sql tools, type `\j user pass jdbc:hsqldb:file:gtfs`

### Postgresql
(assumes version 9.3 & 9.1.13 on unbuntu 12.04. And making sure username and password.)
```bash
java -classpath onebusaway-gtfs-hibernate-cli-1.3.3.jar:postgresql-9.3-1100.jdbc4.jar \
 org.onebusaway.gtfs.GtfsDatabaseLoaderMain \
 --driverClass=org.postgresql.Driver \
 --url=jdbc:postgresql://localhost/gtfs \
 --username=postgres \
 --password= \
 ../data/google_transit.zip
```

### Mysql
(Is similar to Postgresql for details go https://groups.google.com/forum/#!topic/onebusaway-developers/3Qhf7QRU9wI)
