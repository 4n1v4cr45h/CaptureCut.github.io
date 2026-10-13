---
title: Fierce
id: 015
---

Fierce is a DNS reconnaissance tool for locating non-contiguous IP space. It can be used to identify potential hosts and subdomains within a target domain, as well as to perform DNS lookups on specific IP ranges or subdomains.

Here are the available options for the fierce command:


-h, --help : Show this help message and exit.

--domain DOMAIN : Domain name to test.

--connect : Attempt HTTP connection to non-RFC 1918 hosts.

--wide : Scan entire class C of discovered records.

--traverse TRAVERSE : Scan NUMBER IPs before and after discovered records. This respects Class C boundaries and won't enter adjacent subnets.

--search SEARCH [SEARCH ...] : Filter on these domains when expanding lookup.

--range RANGE : Scan an internal IP range, use CIDR notation.

--delay DELAY : Time to wait between lookups.

--subdomains SUBDOMAINS [SUBDOMAINS ...] : Use these subdomains.

--subdomain-file SUBDOMAIN_FILE : Use subdomains specified in this file (one per line).

--dns-servers DNS_SERVERS [DNS_SERVERS ...] : Use these DNS servers for reverse lookups.

--dns-file DNS_FILE : Use DNS servers specified in this file for reverse lookups (one per line).

--tcp : Use TCP instead of UDP.

You can use the -h option to display this help message and exit, or you can use the --help option to display the help message and continue running the command.
