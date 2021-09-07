---
layout: post
title: Why, What, and How of DNS
tags: why-what-how
so: dns/stackoverflow.png
host: dns/host.png
addressing: dns/addressing.jpeg
domains: dns/domains.png
res: dns/name-res.jpeg
---

Programs can find web pages, mailboxes, and other resources using the IP addresses of their servers. An IP address looks like `128.111.24.11`.  Although these plain IP addresses are convenient for computers, they pose quite a few drawbacks for humans. 

1. They are difficult for people to remember and match against resources. 
2. If a resource changes the server, e.g. a web page moves from one web server to another with a different IP, all users need to update the stored IP address. 

To address the first problem, we use a high-level, readable name to decouple the server name from the server IP address. This allows us to use a friendly, consistent name for a server, regardless of its IP address. 

For example, we can refer to the popular question-answer website StackOverflow using a human-readable address `https://stackoverflow.com` instead of its IP address. 

<a target="_blank" href="{{ site.images }}/{{ page.so }}">
  <img src="{{ site.images }}/{{ page.so }}" alt="Stack Overflow">
</a>  

However, this solution creates another challenge: **how do we convert a human-friendly name to a computer-friendly IP address?** It also doesn't answer the second problem where a resource changes the server. **How do we keep the names up-to-date?**

The solution for all the above problems is to use a system that maps individual IP addresses to human-friendly names and keeps them up-to-date. Any application program that needs to locate the physical address of a resource has to query this system to get its IP address. 

A simple system would just be a centralized text file listing the computer names and their IP addresses. An administrator updates the file whenever a computer changes the IP address. All clients download this file every day to have the most recent information available to them. 

<a target="_blank" href="{{ site.images }}/{{ page.host }}">
  <img src="{{ site.images }}/{{ page.host }}" alt="Host File">
</a>

For a small network, this approach works well. However, with millions of servers connected to the Internet, it fails. First, the size of the file becomes too large and impossible to maintain. Second, the names would constantly conflict unless the file was centrally managed. This is practically impossible on the Internet, due to load and latency. 

To solve these concerns, DNS (Domain Name System) was invented in 1983 by [Paul Mockapetris](https://internethalloffame.org/inductees/paul-mockapetris). It has been a core part of the Internet ever since. 

**What is DNS?**

DNS is a hierarchical, domain-based naming scheme with a distributed database for implementing this naming scheme. The Internet uses it to map host names to IP addresses, but it can be used for other purposes. RFC 1034 introduces the DNS, and RFC 1035 describes it in detail, including its implementation and specification.

DNS manages the host names and IP addresses similarly to how the postal system manages people's names with their home addresses.  Multiple people can have the same name. Hence the postal office manages names by requiring letters to specify the country, state, city, street, and name. This is an example of a hierarchical addressing system. 

Conceptually, the Internet is divided into more than 250 top-level domains, which are further partitioned into subdomains, and so on. Each domain covers many hosts. The following tree diagram represents this structure. A leaf domain may contain a single host, or it may represent an organization and contain thousands of hosts. 

<a target="_blank" href="{{ site.images }}/{{ page.addressing }}">
  <img src="{{ site.images }}/{{ page.addressing }}" alt="Hierarchical Addressing">
</a>

The top-level domains are divided into two types: generic and countries. The generic ones include the original ones from the 1980s, e.g. .com, .org, etc. The country domains include one for each country. The top-level domains are run by registrars appointed by ICANN (Internet Corporation for Assigned Names and Numbers). 

**DNS Records**

Every domain can have a set of resource records associated with it, forming the DNS database. The most common resource record is just its IP address. A resource record consists of the following five elements. 

1. Domain_name: The domain to which this record applies. Many records can exist for a single domain. 
2. Time_to_live (seconds): Indicates how long a client should use/cache this record. A large number indicates a stable domain that doesn't change often. A low value indicates a volatile domain. A very common value is 86400, which is the number of seconds in a day. 
3. Class: Set to IN for Internet records. Rarely used for anything else. 
4. Type: Tells what kind of record this is, e.g. `A, AAAA, NS, CNAME, TXT,` etc. 
5. Value: Value of the record. Depending on the record type, it can be a domain name, a number, or an ASCII string.

Here are the most important types of DNS records. 

- A (Address): Holds a 32-bit IPv4 address for a host. 
- AAAA: Holds a 128-bit IPv6 address for a host. 
- MX: Name of the host prepared to accept email for this domain. Not every machine can accept email. 
- NS: Specifies a name server for the domain. A name server has a copy of the database for this domain. The client uses the name server to look up names. 
- CNAME: Used to create aliases. 
- TXT: Allows domains to identify themselves in arbitrary ways. 

**Name Servers**

A name server is a computer containing the DNS database. In theory, a single name server could contain the entire DNS database, responding to all queries. However, similar to the text file we saw earlier, it won't scale. If it ever goes down, the whole Internet would go down. 

To add resiliency and scalability, the DNS namespace is divided into various zones. Each zone is associated with one or more name servers, which hold the database for that zone. 

Typically, there will be one primary name server, and one or more secondary name servers for backup and reliability. The primary name server gets the information from a file on its disk, and the secondary ones get their information from the primary server. 

**Name Resolution** 

The process of looking up a domain name and fetching its address is called name resolution. When a client has a query about a domain name, it checks the local name server. If the domain falls under the jurisdiction of the local name server, it returns the authoritative resource records, which are always correct and up-to-date. 

If the domain is remote and there's no cached information in the local name server, the name server begins a remote query. It first asks one of the root name servers, containing the information about each top-level domain. 

> *Note: To contact the root server, the local name server must know about the root server. This information is typically present in a sysconfig file on the name server. It's loaded onto the DNS cache when the server starts. It's simply a list of A records for the root.* 

There are 13 root DNS servers, named `a.root-servers.net` through `m.root-servers-.net`, hosted on powerful and heavily replicated computers, present in multiple geographical locations. 

<a target="_blank" href="{{ site.images }}/{{ page.domains }}">
  <img src="{{ site.images }}/{{ page.domains }}" alt="Domains">
</a> 

When the local name server contacts one of the root servers, it returns the address of the name server for the top-level domain name, e.g. .edu, .com, etc.  The local server then continues its search by asking the name server of the top-level domain, until it finds the address of the domain it's looking for. The following diagram illustrates this process:

<a target="_blank" href="{{ site.images }}/{{ page.res }}">
  <img src="{{ site.images }}/{{ page.res }}" alt="Name Resolution">
</a> 

DNS uses the UDP protocol for queries and responses. If no message arrives within a short time, the DNS client repeats the query, trying another server for the domain after a small number of retries. This process ensures that the client gets a response even if a server is down. 

**Caching**

All the intermediate results are cached on the respective servers. Hence, if the same query comes again, that server can respond directly without consulting another name server. 

Though caching greatly reduces the number of queries, improving performance, it doesn't always return the most up-to-date results, as the entry might have been updated in the authoritative name server. For this reason, cache entries don't live too long. The exact time after which they should expire is specified in the `Time_to_live` field in each resource record.  That tells the intermediate name servers how long to cache records. 

**Conclusion**

DNS provides the mapping between human-readable domain names and the IP addresses of machines. It is a large and complex distributed system comprising millions of name servers working together. It provides replication and caching for high performance and reliability. It's highly robust and reliable, and forms an essential part of the Internet infrastructure. 
