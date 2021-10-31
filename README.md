# How to point GoDaddy Domains to DigitalOcean with Cloudflare

How I point any domain to my hosted website on Digital Ocean. In this post I will be pointing GoDaddy domain to DigitalOcean.

You need to have the following requirements:

1.  A domain.
2.  Cloudflare account.
3.  Your hosted website on DigitalOcean.

If you do not have 1 and 2 from the requirements list, go ahead and register one with any domain providers of your choice and create a Cloudflare account. This setup here will apply for any domain provider. Lets jump right into it.

### DigitalOcean

Lets add our GoDaddy domain on DigitalOcean

![DigitalOcean 2021-10-31 23-16-18-618.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/DigitalOcean_2021-10-31_23-16-18-618.jpg)

After adding the domain, we need to add two new records @ and www to the existing records.

![digitalocean-dns 2021-10-31 23-32-54-957.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/digitalocean-dns_2021-10-31_23-32-54-957.jpg)

### Then Cloudflare.

Go to Cloudflare and login or create new account, you should see your Cloudflare dashboard and then add a new domain.

![dashboard 2021-10-31 22-59-38-712.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/dashboard_2021-10-31_22-59-38-712.jpg)

Next enter the domain name.

![add-new-domain 2021-10-31 15-15-38-793.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/add-new-domain_2021-10-31_15-15-38-793.jpg)

![bandicam 2021-10-31 15-17-34-103.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/bandicam_2021-10-31_15-17-34-103.jpg)

Now this part is **important,** you have to add DigitalOcean nameservers to Cloudflare, the **name** and **IPv4** which you can locate from your DigitalOcean networking → domains → domain-name under DNS records, which is the IPv4 given to eg Droplet that you us to SSH via terminal.

Lets add two records that we recently added in DigitalOcean.

1. Click Add record
2. Type: **A** Name: **@** IPv4 address: **134.122.92.145**
3. Type: **A** Name: **www** IPv4 address: **134.122.92.145**

![bandicam 2021-10-31 15-23-19-786.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/bandicam_2021-10-31_15-23-19-786.jpg)

Copy the provided Cloudflare nameservers and **Replace these on your custom domain's nameservers** from your domain provider in our case GoDaddy.

![nameserver-names.png](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/nameserver-names.png)

GoDaddy

Under **_My domains_**

Then **\*Domain settings** you should see the domain DNS information nameservers managed by your\* provider.

![godaddy-2021-10-30 16-14-38-067.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/godaddy-2021-10-30_16-14-38-067.jpg)

Click change button

Then select **I'll use my own nameservers**

![godaddy-dns-management 2021-10-31 22-46-41-857.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/godaddy-dns-management_2021-10-31_22-46-41-857.jpg)

Now let go back to Cloudflare to confirm that our setup is successfully If the **Name Server** output is correct, select **Re-check now**.

![Cloudflare check nameserver 2021-10-31 23-40-39-800.jpg](How%20to%20point%20GoDaddy%20Domains%20to%20DigitalOcean%20with%20%2058e9896a756741fcbeeafb8adb7e74fd/Cloudflare_check_nameserver_2021-10-31_23-40-39-800.jpg)

How to check if your domain nameservers are now pointing to Cloudflare

- You can use these command:

```
*Linux/Unix*
dig domain_name +trace @1.1.1.1
dig domain_name +trace @8.8.8.8

*Windows*
nslookup domain_name 1.1.1.1
nslookup domain_name 8.8.8.8
```

You can also use online tools, such as [https://www.whatsmydns.net/](https://www.whatsmydns.net/)
