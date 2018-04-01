## Installing OCI8 extension for PHP Oracle development

If you’re installing this extension on your server make sure you have **sudo** privilege most of the command required admin privilege .

### These steps are done on the following system:
- CentOS Linux release 7.4.1708 (Core)
- PHP version: 5.6.30 
- Apache Server
----------
### Installation Steps

 1. Download instantclient files
 [http://www.oracle.com/technetwork/database/enterprise-edition/downloads/linuxx86-64soft-092277.html](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/linuxx86-64soft-092277.html)
 **or**
 [http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html)
 
 2. Create a directory for Oracle instant client and move installation files
 
	```bash
	mkdir /opt/oracle
	mv instantclient-basic-linux.x64-12.2.0.1.0.zip /opt/oracle/instantclient-basic-linux.x64.zip
	mv instantclient-sdk-linux.x64-12.2.0.1.0.zip /opt/oracle/instantclient-sdk-linux.x64.zip
	cd /opt/oracle
	unzip /opt/oracle/instantclient-basic-linux.x64.zip
	unzip /opt/oracle/instantclient-sdk-linux.x64.zip
	```
3. Creating symlink for Oracle instant client
	```bash
	ln -s /opt/oracle/instantclient_12_2/libclntsh.so.12.1 /opt/oracle/instantclient_12_2/libclntsh.so
	ln -s /opt/oracle/instantclient_12_2/libocci.so.12.1 /opt/oracle/instantclient_12_2/libocci.so
	```
 4. Now we have to configure dynamic linker run time bindings
	```bash
	echo /opt/oracle/instantclient_12_2 > /etc/ld.so.conf.d/oracle-instantclient
	```
5. Update the Dynamic Linker Run-Time Bindings
	```bash
	ldconfig
	```
6. Install Additional packages required for Oracle Instant Client.
	```bash
	sudo yum install php-pear php5-dev build-essential libaio1
	pecl install oci8-2.0.10
	```
	The above command will ask for the Oracle instant client library path, it should be
	`instantclient,/opt/oracle/instantclient_12_2`

7. Add the OCI8 extension to our php.ini files
	```bash
	echo "extension = oci8.so" >> /usr/local/php/php.ini
	```
	if you are not sure about php.ini path use the following command to find the path
	```bash
	locate php.ini
	```
8. Now we just need to restart our Apache server.
