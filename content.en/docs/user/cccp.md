---
weight: 1
bookFlatSection: true
title: "CCCP"
---
CCCP is the official Soviet Linux package manager, capable of installing .ecmp files.

We'll be utilizing the [CCCP package manager](https://github.com/Soviet-Linux/CCCP) (CCCP Crafter of Controlled Packages). This package manager can use .ecmp files to build source packages or a tar.gz archive with precompiled binaries.

**Options:**
- Regular options:
  - `install`: Install a package from the repos.
  - `package`: Install a package file.
  - `remove`: Uninstall a package.
  - `list`: List all packages.
  - `check`: Check if a package is installed.
  - `help`: Print a help message.
  - `sync`: Synchronize package files.

**Configuration:**
The config file, usually located at `/etc/cccp.conf`, can be used to configure the CCCP. You can change the CCCP's root path and specify package repositories.
