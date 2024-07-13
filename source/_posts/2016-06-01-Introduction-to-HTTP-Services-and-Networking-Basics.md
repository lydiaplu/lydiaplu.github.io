---
title: Introduction to HTTP Services and Networking Basics
date: 2016-06-01 12:50:17
toc: true
categories:
- AJAX

---

**Content**: Introduction to servers, networking basics, and software architecture.
<!--more-->

## 1. Servers

> Introduction: In simple terms, a machine (computer) capable of providing a certain service is called a server.

#### 1.1 Types of Servers

Servers can be categorized based on various criteria:

1. Based on **service type**, servers can be file servers, database servers, mail servers, web servers, etc.
2. Based on **operating system**, servers can be Linux servers, Windows servers, etc.
3. Based on **application software**, servers can be Apache servers, Nginx servers, IIS servers, Tomcat servers, weblogic servers, WebSphere servers, boss servers, Node servers, etc.

#### 1.2 Server Software

Server software refers to application software that enables a computer to provide a specific service. By installing the corresponding server software and configuring it, a computer can gain the ability to provide a particular service.

Common server software includes:

1. File Servers: Server-U, FileZilla, VsFTP, etc. (FTP - File Transfer Protocol)
2. Database Servers: Oracle, MySQL, SQL Server, DB2, Access, etc.
3. Mail Servers: Postfix, Sendmail, etc.
4. **HTTP Servers**: Apache, Nginx, IIS, Tomcat, Node.js, etc.

#### 1.3 HTTP Servers

HTTP servers, commonly referred to as web servers, primarily provide document (text, images, videos, audio) browsing services. They are typically configured with Apache or Nginx server software.

HTTP servers can be used in conjunction with a programming language to handle business logic, leading to server-side development. Common programming languages for server-side development include PHP, Java, .NET, Python, Ruby, Perl, and more.

## 2. Clients

Clients are devices capable of requesting services from servers. Examples include mobile phones, computers, etc. By installing different client software, clients can access various services. For instance, QQ provides instant messaging services, while Thunder allows downloading.

Common client software includes web browsers, QQ, Thunder, Foxmail, etc.

Front-end development refers to a series of development tasks carried out using browsers as the hosting environment and technologies like HTML, CSS, JavaScript, etc.

## 3. Networking Basics

#### 3.1 IP Address

An IP address is a 32-bit address assigned to each host connected to the internet. It serves as a unique identifier for each device on the network, similar to how phones have unique numbers.

You can check your local IP address using commands like `ping`, `ipconfig` (Windows), or `ifconfig` (Linux).

**IP addresses can be divided into two types:**

1. Local IP: Assigned by switches or routers within a specific area, forming a computer group.
2. Public IP: Usually obtained through an application process with a telecom provider and may require a business license.

#### 3.2 Domain Names

Domain names are used to represent IP addresses, making them easier to remember. A domain name is like a mask for an IP address.

You can check the IP address associated with a domain name using the `ping` command.

**Domain names have different types:**

e.g., .com, .net, .com.cn, .gov

A domain can have multiple subdomains.

To use a domain, you need to register it, and for public access, you may need to apply for an ICP (Internet Content Provider) license from the local government. The approval process usually takes around a week. Some websites can be accessed via their IP addresses, but these are often gray area websites.

#### 3.3 DNS Service

DNS (Domain Name System) is a distributed database on the internet that maintains the mapping between domain names and IP addresses. DNS servers help resolve domain names into their corresponding IP addresses.

DNS lookup priority: Local hosts file > DNS server

To refresh DNS cache, use the command `ipconfig /flushdns`.

#### 3.4 Ports

In computer networking, a port serves as an endpoint for communication between two computers. Ports allow a single physical network connection to be used by multiple processes.

For example, web services use port 80 by default, while MySQL uses port 3306.

## 4. Software Architecture

#### 4.1 Client/Server Architecture (C/S)

In a client/server architecture, communication occurs between clients and servers. Clients request services from servers, which then respond.

**C/S Workflow Diagram**
![C/S Workflow Diagram](/images/8-1/CS工作流程图.png)

Different services may require the installation of different client software. For instance, to use QQ for instant messaging, you need to install the QQ client.

#### 4.2 Browser/Server Architecture (B/S)

In a browser/server architecture, all services can be accessed through a web browser. This eliminates the need to install multiple client software.

While B/S architecture is convenient, it may have limitations in terms of stability and performance compared to C/S architecture.