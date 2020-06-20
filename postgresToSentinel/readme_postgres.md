# Install a PostgreSQL database on Ubuntu for testing out the Logstash postgres-to-sentinel pipeline

## Install PostgreSQL

    sudo apt-get install postgresql

## Create database user

    su - postgres

    createuser --interactive --pwprompt

At the Enter name of role to add: prompt, type the <username>.

At the Enter password for new role: prompt, type a password for the user.

At the Enter it again: prompt, retype the password.

At the Shall the new role be a superuser? prompt, type y if you want to grant superuser access. Otherwise, type n.

At the Shall the new role be allowed to create databases? prompt, type y if you want to allow the user to create new databases. Otherwise, type n.

At the Shall the new role be allowed to create more new roles? prompt, type y if you want to allow the user to create new users. Otherwise, type n.
PostgreSQL creates the user with the settings you specified.

## Create database and table

    psql

    CREATE DATABASE security;
    
### list all databases

	\l

### list all tables

	\dt

### create table

	CREATE TABLE authentication (uid serial,timestamp TIMESTAMP,event VARCHAR(80) NOT NULL,message VARCHAR(80) NOT NULL,username VARCHAR(80) NOT NULL,ipaddress VARCHAR(80) NOT NULL);

### quit psql

	\q

## Grant database user on database

    GRANT all privileges ON DATABASE security to <username>;

## Insert some data

	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-16 19:26:25', '1010', 'User succesfully logged in', 'koos', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-16 19:26:25', '9050', 'User changed password', 'koos', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-16 19:25:57', '9000', 'Password expired, needs to be changed', 'koos', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-16 19:25:54', '500', 'Incorrect password, access denied', 'koos', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-16 19:25:50', '500', 'Incorrect password, access denied', 'koos', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-16 19:25:47', '500', 'Incorrect password, access denied', 'koos', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-11 15:11:23', '1010', 'User succesfully logged out', 'lutsdbadmin', '213.115.102.6');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-11 15:11:12', '1000', 'User succesfully logged in', 'lutsdbadmin', '213.115.102.6');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-05 04:05:21', '115', 'Access denied! Unknown IP', 'dbtest', '73.85.10.46');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-05 04:05:21', '115', 'Access denied! Unknown IP', 'test', '73.85.10.46');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-05 04:05:19', '115', 'Access denied! Unknown IP', 'dbo', '73.85.10.46');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-05 04:05:18', '115', 'Access denied! Unknown IP', 'administrator', '73.85.10.46');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-05 04:05:17', '115', 'Access denied! Unknown IP', 'administrator', '73.85.10.46');

## Insert some more data after Logstash finished its initial query and upload

	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 14:02:32', '115', 'Access denied! Unknown IP', 'admin', '212.10.115.6');
	
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 14:11:02', '115', 'Access denied! Unknown IP', 'admin', '212.10.115.6');
	
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 15:01:32', '115', 'Access denied! Unknown IP', 'admin', '164.1.212.1');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 15:02:43', '115', 'Access denied! Unknown IP', 'administrator', '164.1.212.1');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 15:04:57', '115', 'Access denied! Unknown IP', 'test', '164.1.212.1');
	
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 15:31:23', '1010', 'User succesfully logged out', 'lutsdbadmin', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 15:42:12', '1000', 'User succesfully logged in', 'lutsdbadmin', '178.85.181.163');

	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 15:45:13', '1010', 'User succesfully logged in', 'lutsdbadmin', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-17 15:50:31', '1000', 'User succesfully logged out', 'lutsdbadmin', '178.85.181.163');
	
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-18 11:15:50', '500', 'Incorrect password, access denied', 'koos', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-18 11:16:02', '1010', 'User succesfully logged in', 'lutsdbadmin', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-18 11:31:31', '1000', 'User succesfully logged out', 'lutsdbadmin', '178.85.181.163');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-18 16:01:32', '115', 'Access denied! Unknown IP', 'admin', '71.217.91.7');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-18 16:02:43', '115', 'Access denied! Unknown IP', 'administrator', '71.217.91.7');
	INSERT INTO authentication(timestamp, event, message, username, ipaddress) VALUES('2020-04-18 16:04:57', '115', 'Access denied! Unknown IP', 'test', '71.217.91.7');
