# acme.sh Previder DNS

This guide explains how to use **acme DNS validation** in combination with **Previder DNS**.

# Step 1 – Install acme.sh

```bash
curl https://get.acme.sh | sh -s email=my@example.com
```
Replace my@example.com with your actual email.

## Step 2 – Generate an API key

A **Previder Portal [user](https://portal.previder.nl/#/user/current/tokens) or [application](https://portal.previder.nl/#/application) token** is required to modify DNS records and request certificates.

The token must have the following privileges:

- **Read** on Domains  
- **Read/Update** on DNS for the client  

This token will be visible to anyone who has access to the server.  
Create a dedicated role with only the required privileges for secure operation.

# Step 3 – Configure Previder DNS
First you need to login to your PowerDNS account to enable the API and set your API-Token in the configuration.
```bash
export PDNS_Url="https://portal.previder.com"
export PDNS_ServerId="previder"
export PDNS_Token="YOUR_API_KEY_HERE"
export PDNS_Ttl=60
```
Replace `YOUR_API_KEY_HERE` with your actual API key.

# Step 4 – Test the configuration (dry run)
Ok, let's issue a cert now:
```bash
./acme.sh --test --issue --dns dns_pdns -d example.com -d *.example.com 
```
The PDNS_Url, PDNS_ServerId, PDNS_Token and PDNS_Ttl will be saved in ~/.acme.sh/account.conf and will be reused when needed.
