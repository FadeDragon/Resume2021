# Contents
- Diagram and related scripts for cognito user pool

- Lambda for API gateway used as the AWS transfer instance's custom identity provider

*Note that the above will be used by an instance in AWS transfer family*

# Proof of concept - Background
Orders from clients are usually done via a web interface. An FTP service allows clients to directly upload their orders without going through the web interface and trigger the same processing.

## Currently
Existing service was built in-house using a public facing EC2 instance with an FTP server installed on it. It stored the orders locally and sometimes ran out of disk space during periods of high traffic.

Sometime last year, one of the clients wanted to improve security for their content and has requested for SFTP to be made available, along with private key authentication.

## Overview of proposal
From the business' point of view, the requirement is to ensure all clients can use this service regardless of whether they are migrating to SFTP or not. From the development point of view, the FTP server can easily take on a new protocol which is SFTP.

But from the architecture point of view, this is an opportunity to push for a solution that requires lower maintenance effort and does not run out of space. AWS Transfer Family is a great candidate as it is a managed service which seamlessly works with S3 storage.

### Diagrams
Diagram for AWS resources

![AWS resources](https://github.com/FadeDragon/Resume2020/blob/master/Proof%20of%20concept%20-%20SFTP%20endpoint/ftp%20resources.svg)

### Detailed steps of proposal
Discussion with stakeholders over deciding on a build-or-buy solution for the requirement.

Formal proposal with working proof of concept.
* Use the following link to setup a password enabled SFTP instance
* https://aws.amazon.com/blogs/storage/enable-password-authentication-for-aws-transfer-for-sftp-using-aws-secrets-manager/
* Requirements from management is to use cognito instead of secrets manager to store user login details


Coordinate with product, development and support teams to allow said client to switch to SFTP while ensuring other clients carry on with FTP.


