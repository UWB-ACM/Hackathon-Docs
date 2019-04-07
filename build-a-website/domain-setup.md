---
title: Obtain A Domain Name and Redirect Domain DNS
layout: topic
categories: guide
---

Now that you have a webpage and are ready to deploy it, you need to 
set up a domain name for your website. This wiki will walk you through 
that process.

## Step 1: Obtain a Domain Name

It is recommended to get a domain name off of [NameCheap](https://www.namecheap.com), 
but you can purchase a domain name from other providers (including 
[GoDaddy](https://www.godaddy.com/) and [HostGator](https://www.hostgator.com/domains)).

To get your domain name:
- Create an account with the provider of your choosing.
- Pick a name that sounds good to you. NameCheap has convenient search 
  functionality to help you find the perfect domain name for your 
  project.
- **For NameCheap:** select [WhoIsGuard](https://www.namecheap.com/support/knowledgebase/article.aspx/278/37/what-is-whoisguard) 
as an option when you are going through checkout. This is a free 
service that NameCheap provides that protects your personal information 
when other people run `whois` on your domain name.
- Purchase the domain name.

And you're done!

_Note: avoid purchasing extra paid services (like NameCheap's PremiumDNS 
service); these add-on purchases are not necessary with adequate site 
configuration and a little know-how._

## Step 2: Forward the Domain Name to a DNS Provider

If you are using Digital Ocean to host your site (as recommended in 
the [hackathon docs](Server-Creation)), you can set up domain name 
system (DNS) forwarding to Digital Ocean directly. The required steps 
are described in detail [here](https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars).

Here's a quick run-down of the steps involved:
- Log into your domain purchasing site (in this example, we'll use 
  NameCheap).
- Go to the management page for the domain you bought. In NameCheap, 
  this will be under [Dashboard](https://ap.www.namecheap.com/dashboard).
- Under the domain you bought, click "Manage".
- Under the "Nameservers" section, select "Custom DNS" in the dropdown, 
  and add the server URLs for Digital Ocean. They are 
  `ns[1-3].digitalocean.com`. The end result should look like this:
  ![NameCheap DNS forwarding](./images/namecheap_dns.png).
- Click the green check mark to save the DNS settings for the domain.

After saving, you will see a confirmation alert, and the alert will 
tell you the DNS server update may take up to 48 hours to take effect. 
Don't panic; normally DNS changes propogate in 30-45 minutes.

If you choose to use another provider, you may have to forward the 
domain to a third-party DNS provider; we recommend using 
[Hurricaine Electric](https://dns.he.net/) because it is free, secure, 
easy to use, and informative.

## 

Possibly cut from docs:
- DNS record type information here https://en.wikipedia.org/wiki/List_of_DNS_record_types
