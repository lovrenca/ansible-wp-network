# Ansible wp role

In the current state this ansible role fetches the necessary certificates and creates nginx configuration for wordpress sites.
It is meant for mass configuration of wordpress sites

## Dependencies

* [Ansible letsencrypt](https://github.com/lovrenca/ansible-letsencrypt) - Fetches certificates from letsencrypt.
* [Ansible nginx](https://github.com/lovrenca/ansible-nginx) - Sets up nginx and configures it.

## Variables:
* wp_network_microsites - object with:
  * name - String representing site domain name
  * domains - list of domains for this site. The first domain listed will be the address, others will redirect to it.

## Usage
This ansible role presumes the following:
* You have wordpress setup on the server behind the upstream `wp-http-pass`.
* You have DNS records for the domains you wish to point at it configured.
This is most likelly a dockerized wordpress.
To add sites for this wordpress network, you must simply add them to the wp_network_microsites variable.
this will look like:
```
wp_network_microsites:
  - name: example.com
    domains:
      - example.com
      - www.example.com
```
As mentioned the first domain will be the main one and the other ones will redirect to it.
Certificates will be fetched for all listed domains. Name can be any string but domain name is recommended.

## TODO
Setup wordpress and configure wordpress network
