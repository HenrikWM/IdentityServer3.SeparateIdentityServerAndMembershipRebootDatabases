IdentityServer3.SeparateIdSrvConfigAndMembershipRebootDatabases
===============================================================

This repository combines the two following **IdentityServer** sample projects for **MembershipReboot** and **EntityFramework** into one single project that has separate **MembershipReboot** and **IdSrv3Config** databases.

#### EntityFramework [link](https://github.com/IdentityServer/IdentityServer3.Samples/tree/master/source/EntityFramework)
Sample which illustrates how to use the IdentityServer3.EntityFramework plugin which stores all of IdentityServer's configuration in an EF-capable database.

#### MembershipReboot [link](https://github.com/IdentityServer/IdentityServer3.Samples/tree/master/source/MembershipReboot)
Sample which illustrates how to use the IdentityServer3.MembershipReboot plugin for identity management using MembershipReboot.

## Background

There are several good reasons for why you should not store the **IdentityServer** config and **MembershipReboot** userdata in a single database. 

Firstly, you're combining two very different frameworks into a single database with shared data and configuration.

Secondly, with regards to single resposibility, it's not advisable to have **IdentityServer** config in the same database as your **MembershipReboot** userdata. A **MembershipReboot** user management self-service portal will only need to use the **MembershipReboot** database, and use a web-endpoint to your **IdentityServer** for authentication & authorization. If this website's database were to be compromised and your database is shared with **IdentityServer**, the attacker would also gain information on your entire **IdentityServer** configuration! Splitting into two databases also enables you to use two separate database-useraccounts, which is more secure and reduces information available to an attacher should one be compromized.

And lastly, the separate frameworks will evolve independantly and migrations will be easier to handle when there are two databases. Also, if you have database-customizations then this also becomes more manageable with separate databases.
