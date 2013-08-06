Build a more composable composition layer

# Overview

Build a better

# Motivation

In order to meet the future deployment requirements of OpenStack,
we need to build a new model. The current model of both the puppet-openstack
(not the core modules, just the high level composition layer) module as well
as grizzly-manifests will not scale to meet our needs and the needs of the
community and we must create something better.

# Requirements

* support multiple deployment scenarios
* support user specific configurations
* support flexible configuration of multiple backends (plugins)
* support the programmatic specification of deployment scenarios (HA/AIO/etc)
* all components should be composed of each other:
** AIO == (compute + controller + network controller)
* proposed architecture must specify implementation patterns that can be applied by future developers
* should also meet the requirements of the community so that it becomes 'the way'
to deploy openstack with Puppet

# Architectural Components

## hiera

Hiera is an external data lookup system that supports hierarchical
data overrides.

It will be responsible for mapping class parameters of roles to their
desired data values. Initially, this data will be stored in
yaml files.

Hiera is a key to the solution b/c it allows data lookup to occur
separately (and outside) of your puppet content. This means two things:

* classes can be included in multiple locations
* classes do not have to forward their data to other classes.

These characteristics are key to supporting the ability to allow
multiple deployment scenarios to be composed of shared building blocks.

## roles/profiles

Roles/Profiles is a commonly used pattern in Puppet  originally inspired by this
[blog post](http://www.craigdunn.org/2012/05/239/).

### roles

Roles are high level constructs that can be applied to represent
the full role a machine plays.
  ie: quantum-controller, or openstack-compute

It is possible that we will just want our installer UI to generate
roles as yaml.

#### Rules

- Only roles should be assigned to nodes.
- Each node should be assigned only one role.
- Roles may accept parameters, but those parameters may only be used to conditionally determine which profiles are included as a part of the role

### profiles

Used to express the types of services that can be composed to
build roles.

Uses hiera lookups from class parameters.

Hiera is used so that a profile can be applied multiple
times to compose either a profile or role.

Class parameters allow the interfaces to be introspected (
hopefully our UI tool will eventually do this)

## resource_types

The resource type indirection in Puppet supports for the introspection of
all class parameters.

This is an important architectural component for two reasons:

* All externally specified data should be expressed as a class parameter to allow its introspection
* whatever front end we build needs to understand how to introspect this data.

# Process

* define deployment requirements
* determine correct granularity of building blocks
** evaluate granularity of https://github.com/hastexo/kickstack
* write composition layer
* integrate it into integration tests
* propose solution to puppet-openstack community
