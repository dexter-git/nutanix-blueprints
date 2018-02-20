# Nutanix Calm & OpenLDAP

This Nutanix Calm blueprint will deploy OpenLDAP in preparation for use with a Nutanix cluster.

The intention of this blueprint is to allow customers testing of OpenLDAP, a common alternative to Active Directory.

## Components

- 1x OpenLDAP server
- 1x CentOS 7 Linux VM configured to authenticate against the new OpenLDAP directory

## Prerequisites

To deploy this blueprint you will need the following things available.

- A CentOS 7 Linux VM image, published via the Nutanix Image Service
- Username and password for your Linux image (note that this blueprint does not natively use of public/private key authentication)

## Usage

- Import the blueprint into your Nutanix Calm environment
- Adjust credentials to suit your requirements (the import will warn about blueprint validation errors, since credentials are not saved in exported blueprints)
- Alter each Calm service/VM so that it deploys your CentOS 7 image
- Alter each Calm service/VM so that it connects to your preferred network
- Launch the blueprint
- Fill in all required runtime variables, paying particular attention to the credentials section
- After deployment, connect to the deployed Linux client and login with the credentials supplied during deployment