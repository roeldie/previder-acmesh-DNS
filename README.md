# acme.sh Previder DNS

This guide explains how to use **acme DNS validation** in combination with **Previder DNS**.

# Step 1 – Install acme.sh

```bash
curl https://get.acme.sh | sh -s email=my@example.com
```

# Step 2 – Configure Previder DNS
First you need to login to your PowerDNS account to enable the API and set your API-Token in the configuration.
```bash
export PDNS_Url="https://portal.previder.com"
export PDNS_ServerId="previder"
export PDNS_Token="YOUR_API_KEY_HERE"
export PDNS_Ttl=60
```
Replace `YOUR_API_KEY_HERE` with your actual API key.

# Step 3 – Test the configuration (dry run)
Ok, let's issue a cert now:
```bash
./acme.sh --issue --dns dns_pdns -d example.com -d *.example.com
```
The PDNS_Url, PDNS_ServerId, PDNS_Token and PDNS_Ttl will be saved in ~/.acme.sh/account.conf and will be reused when needed.
