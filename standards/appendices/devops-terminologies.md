# DevOps Terminologies

## App servers
App server instances are known to run under a linux operating system.
Most commonly selected distro version of linux would be ubuntu in common cases.
This server instance houses the application and the web server which serves the application.
Think of the physical server of old
For the AWS space, we call them EC2 server instances.

## Web servers
An application server is an application that manages **HTTP** (Hypertext Transfer Protocol) requests and responses.
It also serves **SMTP** (Simple Mail Transfer Protocol). In short, Web servers do the sending and receiving of emails, hosting web pages, managing FTP files, etc.
The process of a web server connected to a network that allows for data access with other users that belong to the network would be called **Client Server model**.
Web servers can also act as a firewall (limiting access to web pages or resources) and add in security via SSL configurations.
Common web servers out in the market are Apache, IIS, Nginx or for Rails engineers, Puma.
For RoR development that runs locally, the default web server used is Puma. For elixir/phoenix apps would be Cowboy. For production level scenarios we commonly use Nginx.


## Relational Database Service (RDS)
Is an AWS service that allows engineers to manage relational databases.
It supports commonly used relational databases such as MySql, PostgreSql, Oracle, MS Sql, NoSQL etc.
AWS RDS supports features such as scaling, replication, data snapshots.
