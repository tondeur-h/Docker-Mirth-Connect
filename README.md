mirth-connect
============

# What is Mirth Connect?

[Mirth® Connect](https://www.mirth.com/Products-and-Services/Mirth-Connect) makes it easy to transform non-standard data into standard formats and to monitor multiple interfaces. Available to use for free under an open source license or with our commercial license, where additional enterprise features and support are at your disposal, it’s designed for seamless healthcare message integration, and is well-tested, delivering the advantages and innovation that comes with a large user base.

# How to build this Image 
	$ docker build --file=Dockerfile.server --tag=ht-mirth37 --force-rm --rm=true .


# How to use this image


## Running Mirth Connect Server

Mirth Connect Server contains the back-end for the management interface and the integration engine component, which performs message filtering, transformation, and transmission.

    $ docker run -d --name HT-Mirth -p 8080:8080 -p 8443:8443 ht-mirth37:latest

## Configuring Mirth Connect Server

Create a configuration file for Mirth Connect Server from the default configuration file in SVN. Update the database properties to connect to a remote MySQL instance.

    $ svn export https://svn.mirthcorp.com/connect/trunk/server/conf/mirth.properties ~/mirth.properties
    $ vim mirth.properties
    ...
    database = mysql
    database.url = jdbc:mysql://prod-cluster.us-west-2.rds.amazonaws.com:3306/mirthdb
    database.username = mirth
    database.password = mirth

Launch the container and mount the configuration file:

    $ docker run -d -P -v ~/mirth.properties:/opt/mirth-connect/conf/mirth.properties brandonstevens/mirth-connect

## Running Mirth graphical Administrator

	http://localhost:8080

