---
source_url: https://northflank.com/docs/v1/application/getting-started/add-a-and-verify-domain
title: Add and verify a domain | Getting Started | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.022224
watsonmd_version: 0.1.0
---

Getting Started / 

# Add and verify a domain

You can add your own domains and subdomains to Northflank to use with your deployed service's public ports.

Domains and subdomains are verified on your Northflank account, so once added you can reassign them to any public port for any deployment on your account.

If you use OVH, Cloudflare, NS1, or Namecheap, check our [specific guides for these domain registrars](../domains/domains-on-northflank#dns-providers).

Add a domain

You can add any domain (for example `one.yourdomain.com`) provided you have the ability to edit the DNS records.

  1. [Click here ](https://app.northflank.com/s/account/domains/new), or open the domains page in your account settings.
  2. Click `add domain`, enter your domain name, and click `add domain`
  3. You will now see the information required to verify your domain, including the `record name` and `record content`. You will need to add this to your DNS records as a text (TXT) record.
  4. Open a new browser tab or window and navigate to your DNS provider
  5. Log in to your control panel and find the DNS settings for your domain
  6. Add a new text (TXT) record with the `record name` and `record content` specified in the entry you just generated for the domain on Northflank
  7. Return to the Northflank domains page and select `verify` on the entry for your domain
  8. Northflank will attempt to verify your domain - if not, check you have entered the record correctly and try again. If you need to, you can close the verification dialogue and come back to it later.



![A verified domain in the Northflank application](https://assets.northflank.com/documentation/v1/application/domains/add-a-domain-to-your-account/domain-verified.png)

Add a subdomain

You can add any subdomain provided you have the ability to edit the DNS records.

  1. [Click here ](https://app.northflank.com/s/account/domains/subdomains/new), or open the domains page in your account settings
  2. Click `add subdomain` and select the root domain name you want to create a subdomain for

  3. Enter the subdomain you want to use and click `create subdomain`

  4. You will now see the information required to verify your domain, including the `record name` and `record content`. You will need to add this to your DNS records as a CNAME, ALIAS, or APEX record (depending on host).

![An unverified subdomain in the Northflank application](https://assets.northflank.com/documentation/v1/application/domains/add-a-domain-to-your-account/subdomain-unverified.png)

  5. Open a new browser tab or window and navigate to your DNS provider

  6. Log in to your control panel and find the DNS settings for your domain

  7. Add a new CNAME record with the `record name` and `record content` specified in the entry you just generated for the subdomain on Northflank

  8. Set the time to live (TTL) as recommended, or as low as you can to make your domain available as soon as possible

  9. Return to the Northflank domains page and select `verify` on the entry for your subdomain

  10. Northflank will attempt to verify your domain - if it doesn't verify, check you have entered the record correctly and try again. If you need to, you can close the verification dialogue and come back to it later.




Link a domain to a port

  1. Open the ports & DNS page on the service that contains the port you want to link and click `edit domains`, or click `link domains` next to the port
  2. Find the domain or subdomain you wish to associate with the service in the list
  3. Select the port from drop-down list next to the subdomain you want to link
  4. Click `save changes`



![Linking a domain to a port on a combined service in the Northflank application](https://assets.northflank.com/documentation/v1/application/domains/link-a-domain-to-a-port/custom-domain.png)

Northflank will automatically generate TLS certificates for your domain or subdomain and your domain should redirect to your specified port soon after saving. You can also manage the ports that your domains are linked to via your account's domains page in your account dashboard.

Learn more about domains on Northflank

[Domains on NorthflankManage your domains on Northflank, quickly and easily assigning them to your deployments.](/docs/v1/application/domains/domains-on-northflank)[Add a domainAdd your domain name to your Northflank account.](/docs/v1/application/domains/add-a-domain-to-your-account)[Use your apex domainUse your apex (root) domain name with a Northflank service.](/docs/v1/application/domains/add-a-domain-to-your-account#add-a-domain)[Link a domain to a portHow to link and unlink domains and subdomains with specific ports on your deployments.](/docs/v1/application/domains/link-a-domain-to-a-port)[Use path-based routingRoute incoming traffic to different services and ports for paths on a subdomain.](/docs/v1/application/domains/use-path-based-routing)[Domain registrar guidesFollow walkthroughs to add and verify domains on Cloudflare, NS1, OVH, and Namecheap.](/docs/v1/application/domains/domains-on-northflank#custom-domains-and-subdomains)