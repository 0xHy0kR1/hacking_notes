   - So you were said that everything belonging to some company is inside the scope, and you want to figure out what this company actually owns.

The goal of this phase is to obtain all the **companies owned by the main company** and then all the **assets** of these companies.

**To do so, we are going to:**
   1. Find the acquisitions of the main company, this will give us the companies inside the scope.
   2. Find the ASN (if any) of each company, this will give us the IP ranges owned by each company.
   3. Use reverse whois lookups to search for other entries (organisation names, domains...) related to the first one (this can be done recursively)
   4. Use other techniques like shodan `org`and `ssl`filters to search for other assets (the `ssl` trick can be done recursively).

### Acquisitions

   - First of all, we need to know which **other companies are owned by the main company**. One option is to visit [https://www.crunchbase.com/](https://www.crunchbase.com), **search** for the **main company**, and **click** on "**acquisitions**". There you will see other companies acquired by the main one.
![[ex_recon1.png]]

   - Other option is to visit the **Wikipedia** page of the main company and search for **acquisitions**.
   - Ok, at this point you should know all the companies inside the scope. Lets figure out how to find their assets.

### ASNs

   - An autonomous system number (**ASN**) is a **unique number** assigned to an **autonomous system** (AS) by the **Internet Assigned Numbers Authority (IANA)**.
   - An **AS** consists of **blocks** of **IP addresses** which have a distinctly defined policy for accessing external networks and are administered by a single organisation but may be made up of several operators.
   - It's interesting to find if the **company have assigned any ASN** to find its **IP ranges.** It will be interested to perform a **vulnerability test** against all the **hosts** inside the **scope** and **look for domains** inside these IPs
   - You can **search** by company **name**, by **IP** or by **domain** in [**https://bgp.he.net/**](https://bgp.he.net)**.** **Depending on the region of the company this links could be useful to gather more data:** [**AFRINIC**](https://www.afrinic.net) **(Africa),** [**Arin**](https://www.arin.net/about/welcome/region/)**(North America),** [**APNIC**](https://www.apnic.net) **(Asia),** [**LACNIC**](https://www.lacnic.net) **(Latin America),** [**RIPE NCC**](https://www.ripe.net) **(Europe). Anyway, probably all the** useful information **(IP ranges and Whois)** appears already in the first link.
