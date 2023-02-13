# active-directory-fundamentals

> The intention of this section is to give an overview of concepts. Specific attack techniques each get their own page.

The goal of Active Directory is to provide domain services to a network (AD DS). This can be thought of as a phonebook or database, or an enterprise's organization chart. Concepts such as authority, access control, networking, and much more can be implemented into computer networks based of the information present in the directory. 

This is an attractive attack surface because if you can control the information inside active directory, then you have control over the environment. 

## Semantics: Domain VS Workgroup

- default domain is `WORKGROUP` or `HOSTNAME`

- WORKGROUP is a LAN of peer to peer machines
	- Microsoft term for any network of peer2peer machines
	- emphasis on PEER; no computer controls others
	- each computer has its own user accounts
	- all devices are part of same subnet
	- limited to 10-20 devices, smaller counts overall

- DOMAIN is a network of objects that share the same Active Directory Databases
	- accounts are DOMAIN wide
	- any device part of domain will acknowledge the account, provided policy
	- there is a domain controller, a DC. Acts as a server to control member objects of the AD
	- devices can be on differing subnets but be part of same DOMAIN
	- 100-1000+ devices, 




## Physical Traits of Active-Directory

### Domain Controllers

- hosts a copy of the AD DS directory store
- provides authentication/authorization service for the domain
- replication, updates to one DC propagate throughout the domain and forest
- admin access to manage user accounts and network resources


### Active Directory Data Store

The AD DS data store is the database files and processes that make up Active Directory. The AD DS data store is the "crown jewels" of the "vip". Protecting/looting these files is the primary objective when considering the domain controller. 


Traits of AD DS data store:

- file named  `ntds.dit`, the crown jewels
- stored in `%SystemRoot%\NTDS` folder 
- includes password hashes
- includes all other Active Directory data too


## Logical Components of Active-Directory

This section mostly of definitions and brief notes.

### AD DS Schema

> Enforces rules about object creation

This contains definitions of objects that can be created. Want to create a user object? The definition exists as part of the AD DS Schema. Which attributes is an object allowed to have? This is defined here too. The AD DS Schema is exhaustive, if a definition for an object, a prototype, does not exist within it then the object cannot be created. 


### Objects

> the fundamental unit, the elements that we will collect, organize and build things with

examples

- Users: enables network resource access
- InetOrgPerson: similar to user, used for compatibility
- Contacts: No network access, enables assigning emails to external users
- Groups: Administrative tool, form collections of objects, theses are similar to Organizational Units
- Computers: Enables authentication and auditing of access to resources
- Printers: physical office, convenience feature for location and use of printers
- Shared folders: enable users to search for shared folders based off of properties

Note that nesting is possible with some of these objects. e.g. a computer can be a member of a group. This feature opens some interesting methods of persistence and evasion, and therefore some important considerations for defenders. 


### Organizational Units (OUs)

> collections which contain any object defined in the AD DS schema. OUs can also contain other OUs. 

This is our first collection that also has an Action associated with it. OUs are the means that allow the management of objects.

OUs are used to:

- represent organization hierarchically and logically
- delegate permission to administer collections of objects
- apply policies, often through inheritance (e.g. nested OUs)


### Domains

> Domains are collections of objects belonging to an organization

- acts as an administrative boundary
- replication boundary between domain controllers
- authentication and authorization boundary, a way to limit scope of access to resources


### Trees

> Trees are collections of domains

- respects a hierarchy structure, parent child relationships between domains
- by default, a two-way transitive trust exists between domains in the same tree. If a path on the graph exists, we have have bidirectional trust
- can be identified by contiguous namespace with the parent domain
- acts very similarly to domain/subdomain found in URLs


### Forests

> Forests are collections of Trees

- Think of two graphs with a central shared node. A path between trees must exist
- Enables trusts between all domains in the Trees of the Forest (unknown default behavior)
- all trees share:
	- common schema
	- common configuration partition
	- common global catalog. think LDAP
	- Enterprise Admins and Schema Admins groups


### Trusts

> this is how users access resources in another domain, there are two principal types of trust


1. Directional
	- Can be bidirectional or unidirectional
	- If domain A trust domain B then domain B can access resources in domain A

2. Transitive
	- This is how we include more than two domains in a "Trust Tree"
	- If A trusts B and B trusts C, then A trusts C


Some general features of trusts:

- All domains in a forest trust each other by default
- Trusts can extend outside the forest




