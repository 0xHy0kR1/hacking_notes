## Trees
- Active Directory supports integrating multiple domains so that you can partition your network into units that can be managed independently.
- If you have two domains that share the same namespace (`thm.local` in our example), those domains can be joined into a **Tree**.
- If our `thm.local` domain was split into two subdomains for UK and US branches, you could build a tree with a root domain of `thm.local` and two subdomains called `uk.thm.local` and `us.thm.local`, each with its AD, computers and users:

![[AD_basics30.png]]

- This partitioned structure gives us better control over who can access what in the domain.
- The IT people from the UK will have their own DC that manages the UK resources only.
- For example, a UK user would not be able to manage US users.
- In that way, the Domain Administrators of each branch will have complete control over their respective DCs, but not other branches' DCs.
- Policies can also be configured independently for each domain in the tree.
- A new security group needs to be introduced when talking about trees and forests.
- The **Enterprise Admins** group will grant a user administrative privileges over all of an enterprise's domains.

## Forests
- The domains you manage can also be configured in different namespaces. Suppose your company continues growing and eventually acquires another company called `MHT Inc.` When both companies merge, you will probably have different domain trees for each company, each managed by its own IT department.
- The union of several trees with different namespaces into the same network is known as a **forest**.

![[AD_basics31.png]]

## Trust Relationships
- at a certain point, a user at THM UK might need to access a shared file in one of MHT ASIA servers. For this to happen, domains arranged in trees and forests are joined together by **trust relationships**.
- In simple terms, having a trust relationship between domains allows you to authorise a user from domain `THM UK` to access resources from domain `MHT EU`.
- The simplest trust relationship that can be established is a **one-way trust relationship**.
- In a one-way trust, if `Domain AAA` trusts `Domain BBB`, this means that a user on BBB can be authorised to access resources on AAA:
![[AD_basics32.png]]

- **Two-way trust relationships** can also be made to allow both domains to mutually authorise users from the other.
- By default, joining several domains under a tree or a forest will form a two-way trust relationship.
- It is important to note that having a trust relationship between domains doesn't automatically grant access to all resources on other domains.