---
title: Duck DNS
description: Keep your computer registered with the DuckDNS dynamic DNS.
ha_category:
  - Network
ha_iot_class: Cloud Polling
ha_release: 0.55
ha_domain: duckdns
ha_integration_type: integration
related:
  - docs: /docs/configuration/
    title: Configuration file
---

The DuckDNS {% term integration %} allows you to keep your DuckDNS subdomain always in sync with your public IP address, whether IPv4 or IPv6. [DuckDNS](https://www.duckdns.org) is a free service that allows you to bind your own favorite subdomain under `duckdns.org` to the public IP address in use from your router, even though such address is dynamically allocated by your internet service provider and therefore changes over time.

{% warning %}

If you are running the Home Assistant DuckDNS add-on this integration is not required. The add-on will keep your IP updated with DuckDNS.

{% endwarning %}

## Configuration

To use the integration in your installation, add the following to your {% term "`configuration.yaml`" %} file.
{% include integrations/restart_ha_after_config_inclusion.md %}

```yaml
# Example configuration.yaml entry
duckdns:
  domain: YOUR_SUBDOMAIN
  access_token: YOUR_ACCESS_TOKEN
```

{% configuration duckdns %}
  domain:
    description: Your duckdns subdomain (without the `.duckdns.org` suffix).
    required: true
    type: string
  access_token:
    description: Your DuckDNS access token. Log in to the site to get one.
    required: true
    type: string
  ipv4_fetch_url:
    description: The URL used to fetch your IPv4 address.
    required: false
    type: string
    default: "`https://api.ipify.org`"
  ipv6_fetch_url:
    description: The URL used to fetch your IPv6 address.
    required: false
    type: string
    default: "`https://api6.ipify.org`"
  ip_update_mode:
    description: "The IP update mode. Values: `ipv4`, `ipv6`, `both`."
    required: false
    type: string
    default: "`ipv4`"
{% endconfiguration %}

{% important %}
When using custom fetch URLs for IPv4 or IPv6, ensure they are from trusted sources and use HTTPS protocol to prevent potential man-in-the-middle attacks.
{% endimportant %}

## Action `set_txt`

Set the TXT record of your DuckDNS subdomain.

| Data attribute | Optional | Description                 |
| ---------------------- | -------- | --------------------------- |
| `txt`                  | no       | Payload for the TXT record. |
