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

version: The version of the schema
reviewer: RFC5322 name-addr format (eg. John Doe <johndoe@example.com>)
treehash: sha256sum of treehashes
paths: a list of filepaths reviewed or reproduced, can include globs
artifcts: a list of built artificats with hashes if relevant
vcs-ref: VCS ref
type: The type of review. Allowed values are: function, security, readability, reproducibility
system:
  platform:
  cpu:
  cores:
comments: freeform text

## Format

``
version: 0.1
reviewer:
treehash:
paths:
- list of file paths reviewed or reproduced
- supports glob format
artifacts:
- list of built artificats with hashes if relevant
vcs-ref:
type: "function|security|readability|reproduction",
confidence: "low|medium|high"
system:
  platform:
  cpu:
  cores:
  location: "home|aws|gcp|etc"
comments: |
  This is a freeform area
