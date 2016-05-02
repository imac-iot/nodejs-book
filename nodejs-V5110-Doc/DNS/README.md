# Table of Contents

- [DNS](#dns)
  - [dns.getServers()](#dnsgetservers)
  - [dns.lookup(hostname[, options], callback)](#dnslookuphostname-options-callback)
    - [Supported getaddrinfo flags](#supported-getaddrinfo-flags)
  - [dns.lookupService(address, port, callback)](#dnslookupserviceaddress-port-callback)
  - [dns.resolve(hostname[, rrtype], callback)](#dnsresolvehostname-rrtype-callback)
  - [dns.resolve4(hostname, callback)](#dnsresolve4hostname-callback)
  - [dns.resolve6(hostname, callback)](#dnsresolve6hostname-callback)
  - [dns.resolveCname(hostname, callback)](#dnsresolvecnamehostname-callback)
  - [dns.resolveMx(hostname, callback)](#dnsresolvemxhostname-callback)
  - [dns.resolveNs(hostname, callback)](#dnsresolvenshostname-callback)
  - [dns.resolveSoa(hostname, callback)](#dnsresolvesoahostname-callback)
  - [dns.resolveSrv(hostname, callback)](#dnsresolvesrvhostname-callback)
  - [dns.resolvePtr(hostname, callback)](#dnsresolveptrhostname-callback)
  - [dns.resolveTxt(hostname, callback)](#dnsresolvetxthostname-callback)
  - [dns.reverse(ip, callback)](#dnsreverseip-callback)
  - [dns.setServers(servers)](#dnssetserversservers)
  - [Error codes](#error-codes)
  - [Implementation considerations](#implementation-considerations)
    - [dns.lookup()](#dnslookup)
    - [dns.resolve(), dns.resolve*() and dns.reverse()](#dnsresolve-dnsresolve-and-dnsreverse)



# DNS
# dns.getServers()
# dns.lookup(hostname[, options], callback)
### Supported getaddrinfo flags
# dns.lookupService(address, port, callback)
# dns.resolve(hostname[, rrtype], callback)
# dns.resolve4(hostname, callback)
# dns.resolve6(hostname, callback)
# dns.resolveCname(hostname, callback)
# dns.resolveMx(hostname, callback)
# dns.resolveNs(hostname, callback)
# dns.resolveSoa(hostname, callback)
# dns.resolveSrv(hostname, callback)
# dns.resolvePtr(hostname, callback)
# dns.resolveTxt(hostname, callback)
# dns.reverse(ip, callback)
# dns.setServers(servers)
# Error codes
# Implementation considerations
### dns.lookup()
### dns.resolve(), dns.resolve*() and dns.reverse()