## AD DS schema
- Defines every type of object that can be stored in the directory. 
- It enforces rules regarding object creation and configuration 
![[AD_DS_schema.png]]

## Domains
![[AD_domain.png]]
- Domains are used to group and manage objects in an organization.
- An administrative boundary for applying policies to groups of objects.
- A replication boundary for replicating data between domain controllers.
- An authentication and authorization boundary that provides a way to limit the sope of access to resources.

## Trees 
![[AD_DS_tree_domain.png]]
- A domain tree is a hierarchy of domains in AD DS.
- **All domains in the tree:**
	- Share a contiguous namespace with the parent domain.
	- Can have additional child domains
	- By default create a two-way transitive trust with other domains.

## Forests
![[AD_DS_forest.png]]
- A forest is a collection of onr or more domain trees.
- **Forests**:
	- Share a common schema.
	- Share a common configuration partition.
	- Share a common global catalog to enable searching.
	- Enable trusts between all domains in the forest.
	- Share the Enterprise Admins and Schema Admins group.

## Organizational Units(Ous):
- OUs are Active Directory containers that can contain users, groups, computers, and other OUs.
- **OUs are used to**
	- Represent your organization hierarchically and logically.
	- Manage a collection of objects in a consistent way.
	- Delegate permissions to administer groups of objects.
	- Apply policies.

## Trusts:
Trusts provide a mechanism for users to gain access to resources in another domain

1. directional Trusts:
![[AD_DS_directional_trusts.png]]
- A directional trust is a one-way trust relationship established between two domains.
- It allows users from one domain (referred to as the trusting domain) to access resources in another domain (referred to as the trusted domain).
- However, users in the trusted domain do not have automatic access to resources in the trusting domain. In other words, the trust is unidirectional.

**Example**:
consider Domain A and Domain B. If a directional trust is established from Domain A to Domain B, users in Domain A can access resources in Domain B.
However, users in Domain B cannot access resources in Domain A unless a separate trust is established in the opposite direction.

2. Transitive Trusts:
![[AD_DS_transitive_trusts.png]]
- A transitive trust is a two-way trust relationship that can be automatically extended to other domains within the Active Directory forest.
- When a transitive trust is established between two domains, it allows users in both domains to access resources in each other's domains.
- Additionally, the trust relationship can be transitive, meaning it can be passed on to other domains in the forest too.

**Example**:
consider a forest with Domain X, Domain Y, and Domain Z. If a transitive trust is established between Domain X and Domain Y, and another transitive trust is established between Domain Y and Domain Z, then users in Domain X can access resources in Domain Z through the transitive trust relationship.
The trust relationship is automatically extended across domains, allowing users to access resources in any trusted domain within the forest.

## Objects
![[AD_DS_objects.png]]
