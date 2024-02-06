---
layout: default
title: Installation tutorial 
nav_order: 7
---
# Install and configure the REDCap web application

REDCap is primarily a web application, which can be installed on a web server like every other application. In this documentation, we will briefly going through the configuration of the web application.

## Prerequisites

Like every other web application, we need the basic components for a web application.

- A web server, which is a computer used to host the web application.

- A database, which can be installed on a different database server or on the same server as the application.

- Owning a domain for publishing the application

## Install the web application

First, we need to make sure that the web server and the application can interact with each other. Run the following command. In this example, we will assume that we are using MySQL database on a remote server. We will also assume that the web server and database server use CentOS 7 as the default OS.

Install MySQL database and MySQL client on the web server. Install MySQL client on the web server is also needed.

```console
sudo yum install mysqld mysql
```
Run the MySQL database as a service, and start it at startup.

```console
sudo systemctl start mysqld
sudo systemctl enable mysqld
```

Next, we need to install the web service on the web server. We will use Apache HTTPD server in this documentation. Run the following command on the web server to install the web service. We also need to install PHP as the default language for the web server.

```console
sudo yum install httpd
sudo yum install php
```

Start the HTTPD service and run it at startup.

```console
sudo systemctl start httpd
sudo systemctl enable httpd
```

Then, we need to extract the `{redcap_directory}.zip` in the `\var\www\html` directory in the web server. This will be the directory which contains all the files exposed to the web, and run by the web server HTTPD service.

After that, run install.php script in the REDCap folder on the web. You can run the file by using a browser which have access to port 80, access it through localhost `http://localhost/install.php` on the web server or run the following command

```console
curl http://localhost:80/install.php
```

It will display the necessary instruction to install the web application

## Install mail services on the web server

REDCap application requires a working mail service to send transactional mails to user for the web server to fully working. However, this service can be tricky to install correctly. Sometimes, the mail service will fail eventhough the REDCap configuration check tell you that it is working. Our recommendations are:

- Install postfix instead of sendmail for the MTA
- For using external SMTP mail service, consider what is their method of authentication. For example, if you are using Outlook SMTP server for authentication, then you should know that they use STARTTLS protocol for transmissing authentication and information. As a result, it's necessary to provide the username and password to a mail service, as well as providing adequate TLS suite for knowing the Outlook server's public key
