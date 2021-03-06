# Firebird Dockerfile

## Description

Firebird 3.0.2 SuperClassic

### Provides

  Firebird SQL relational database (http://www.firebirdsql.org/).

### Volumes

 * /backup
 * /data

### Exposed Ports

 * 3050

### Env

 * TZ // You can set your timezone via this variable, if not specified then its default value is "Etc/UTC"
 
### Firebird credentials

 * Username: SYSDBA
 * Password: masterkey (only if you didn't specify one via "-e" parametar)

## Run

	$ docker run -d \
		--name firebird \	
		-p 3050:3050 \
		-v /somehostdir/firebird/backup/:/backup/ \
		-v /somehostdir/firebird/data/:/data/ \
        -e FIREBIRD_PASSWORD=secret \
        -e TZ=Europe/Sarajevo \
		mladenp87/firebird-3.0.2-sc

## Misc

### Restore backup

	//enter container console
	$ docker exec -i -t firebird /bin/bash

    //backup
    $ gbak -v -t -user SYSDBA -password masterkey localhost:/data/dbname.fdb /backup/dbname.fbk 

	//restore 
	$ gbak -c -v -user SYSDBA -password masterkey /backup/dbname.fbk localhost:/data/dbname.fdb
