Move code to Gerrit

# Overview

In order to be consistent with upstream openstack, all
Cisco specific Openstack code should be moved to Gerrit.

# Motivation

1. Unifies process for upstream/downstream development.
2. Allows same tools to be leveraged for testing (ie: zuul).
3. It is likely (based on a conversation we had with Monty)
that better community tools for managing upstream/downstream
will be based on federated Gerrits.

# Process

* Look into upstream (openstack-infra) tools that are used to
import content into their Gerrit system.
* Implement these tools
* import our content and change internal processes/documentation
as required.

# Questions

1. Do we need an internal Gerrit System (or can we just use the one provided
by openstack-ingra)?
