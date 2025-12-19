# How domain is configured with the help of domain_name_providers(registrars) and the hosting services

* when user type a domain the DNS servers are queried to resolve the domain to an IP address
* domain_name_providers can edit IP address of the DNS records for that domain
* hosting services have the servers with the static IP addresses where the website files are hosted
* so domain_name_providers need to point the DNS records to the static IP address of the hosting services

## The process of configuring a domain_name_provider to point to hosting service
1. update the DNS records in your domain_name_provider account to point to the static IP(or add CNAME(canonical name) that maps your domain name to the default domain name of project by hosting service) address of your hosting service
2. add your domain name in your hosting service account to link the domain with your hosting service

## Extras
* When a user types a domain name
    1. The browser queries the DNS system to find the IP address associated with that domain.
    2. This query travels through:
        - The root DNS servers,
        - The TLD (Top-Level Domain) servers (like .com, .tech),
        - The authoritative name servers (configured by your domain provider).
* Inside their DNS panel, you can edit records like:
    - A record → points to a hosting IP (e.g., your server)
    - CNAME record → alias (e.g., www → @)
    - MX record → mail servers
    - TXT record → verification, SPF, etc.
* CNAME: domain -> domain
* A record: domain -> IP address