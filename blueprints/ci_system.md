Building a better CI system

# Overview

This document outlines the future plans for building a CI system
capable of testing deployments of Openstack based on multiple
configurations.

# Motivations

Without proper/formalized testing, Cisco cannot reliably deliver
and support features and configurations in its openstack solutions.

Automated tests (esp integration tests) will
- reduce the amount of time it takes to run tests
- ensure that all tests are run to verify regressions continuously

# Plan

## OS AIO server

The build system will start out with an openstack AIO installation.

The rest of the systems will be deployed initially as VMs against this
AIO system.

## Build CI infrastructure

Our CI infrastructure will be based on the following tools:
* gerrit
* zuul
* jenkins/gearman
* jenkins job builder
* caching service (squid?)

Each of these systems will likely run in a VM on top of openstack.

Our CI infrastructure will be deployed using Puppet and borrow
content as much as possible from the openstack-infra team:

  https://github.com/openstack-infra/config


# Process

## build out infrastructure

* build out an AIO server
* ensure that vagrant can target that AIO server
* build out a puppet master
* ensure that vagrant can target the AIO endpoint and build
** build server (jenkins/zuul/gearman/jjb)
** build slave ( do we need a build slave?)
** cache server (squid?)
** AIO

## add more test scenarios

* multi-node (redhat/ubuntu)
* ceph
* swift
* HA

## evaluate triple-o

As we defined our system and understand its code components,
we can begin to evaluate triple-o against those components.

* disk-image-builder can build out base VMs.
** but we should compare it against Packer and VeeWee

