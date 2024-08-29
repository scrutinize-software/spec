# Scrutinize Spec

April 24, 2024

Version: 0.1

## Table of Contents

- [Scruitinize Specification](#scrutinize-spec)
  - [Table of Contents](#table-of-contents)
  - [1 Introduction](#1-introduction)

## 1. Introduction

## 1.1 Scope

This document describes scrutinize, a system for securing the way software is
reviewed. scrutinize attests that software has been independently reviewed. It
does so by providing users an interface

VCS Support

* Git -- `git+`
* Mercurial -- `hg+`
* Subversion -- `svn+`


## Format

| Field Name | Decription | Required |
| :--- | :--- | :---: |
| version | The version of the schema | yes |
| reviewer | RFC5322 name-addr format (eg. John Doe <johndoe@example.com>) | yes |
| treehash | sha256sum of treehashes | yes |
| paths | a list of filepaths reviewed or reproduced, can include globs | yes |
| artifcts | a list of built artificats with hashes if relevant | no |
| vcs-ref | VCS ref | yes |
| type | The type of review. Allowed values are: function, security, readability, reproducibility | yes |
| confidence | How confident are you in the type of review you did: `low,medium,high` | yes |
| system.platform | The platform used to build `amd64,arm64,etc` | yes |
| system.cpu | Information about the CPU used | no |
| system.cores | Number of cores in CPU | no |
| system.location | location of machine(mostly for reproducibility, if in 'the cloud' include the region e.g AWS:us-east-1, could also be ISO 3166-2) | no |
| comments | freeform text | no |

### Security Review Example

```
version: 0.1
reviewer: Danny Grove <danny@dannygrove.com>
treehash: 9cc0641a294d3ee359ae474aef1a9a6a6657aeb2 
paths:
- ./* 
vcs-ref: git+https://github.com/drGrove/mtls-cli
type: "security",
confidence: "high"
system:
  platform: amd64
  location: "ISO3166-2:US-CA"
comments: |
  Very Secure, much wow
```

### Reproducible Build Example(s)

```
version: 0.1
reviewer: Github Action <github-actions[bot]@users.noreply.github.com> 
treehash: a5fc98c3950d7bb6bf083d5e7c08a91ffef990af
paths:
- ./* 
vcs-ref: git+https://git.distrust.co/public/enclaveos
type: "reproducibility",
confidence: "high"
system:
  platform: amd64
  location: "GHA" # Github Actions, if you're using self-hosted runners use the runners code. e.g. AWS:us-west-2
```

```
version: 0.1
reviewer: Danny Grove
treehash: a5fc98c3950d7bb6bf083d5e7c08a91ffef990af
paths:
- ./* 
vcs-ref: git+https://git.distrust.co/public/enclaveos
type: "reproducibility",
confidence: "high"
system:
  platform: amd64
  location: "AWS:us-east-1"
```

```
version: 0.1
reviewer: Danny Grove
treehash: a5fc98c3950d7bb6bf083d5e7c08a91ffef990af
paths:
- ./* 
vcs-ref: git+https://git.distrust.co/public/enclaveos
type: "reproducibility",
confidence: "high"
system:
  platform: amd64
  location: "AWS:us-east-1"
```
