---
weight: 2
bookFlatSection: true
title: "Making Packages"
---
# Making Packages
Soviet Linux uses CCCP. A `.ecmp` file is a recipe that contains all metdata relating to a package, and the
instructions to build the package.

In this guide I will use `bash` as an example.
## Prerequisites:
- [GitHub](https://github.com/signup?ref_cta=Sign+up) account and git
- Understanding the structure of our TOML package file, the ecmp (more info in the following post)
- Basic knowledge of bash scripting, mainly variables
- Understanding basic compiling & installation instructions (`./configure && make && make install`)
- spm-utils

## Clone the OUR

```bash
$ git clone https://github.com/Soviet-Linux/OUR
$ cd OUR
```

## Create package template

Use `mkspm` to create an initial template for your package, then `cd` into its directory. The usage is `mkspm <package name> <package url>`.
in this case its


```bash
$ mkspm bash https://ftp.gnu.org/gnu/bash/bash-5.2.9.tar.gz 
```

The template that is created is as follows:

```
[info]
name = bash
version = 0.0.1
type = src
url = https://ftp.gnu.org/gnu/bash/bash-5.2.9.tar.gz
sha256 = 68d978264253bc933d692f1de195e2e5b463a3984dfb4e5504b076865f16b6dd

[description]

[dependencies]

[download]
curl -L $URL | tar -xz

[install]
./configure
make
make DESTDIR=$BUILD_ROOT install
```

## Packaging format

- `name`: Package name, need same as package's filename (**required**)
- `version`: Package's version (**required**)
- `type`: Package's type, can be src or bin (**required**)
- `url`: Package's source url (**required**)
- `sha256`: SHA-256 of the of URL (**required**)
- `[dependencies]`: All required dependencies, line separated
- `[description]`: Short description for package (Supports markdown)
- `[download]`: Commands that download and extract the source files (**required**)
- `[install]`: all build command should placed in this function (**required**)
- `$BUILD_ROOT`: fake installation directory

> Note: The package's name must be lower-case and cannot contain spaces.

## Edit the package

Edit the `bash.ecmp` to insert any needed variables, information and build commands. Use your favourite
text editor to edit it.

```
$ vim bash.ecmp
```

Here is `bash`'s package file:

```
[info]
name = bash
version = 5.2.9
type = src
url = https://ftp.gnu.org/gnu/$NAME/$NAME-$VERSION.tar.gz
sha256 = 68d978264253bc933d692f1de195e2e5b463a3984dfb4e5504b076865f16b6dd

[description]
The Bourne-Again SHell

[download]
curl -L $URL --output $NAME-$VERSION.tar.gz
tar -xzf $NAME-$VERSION.tar.gz

[install]
./configure --prefix=/usr \
            --without-bash-malloc \
            --with-installed-readline 
make $MAKE_FLAGS
make DESTDIR=$BUILD_ROOT install
```

The package is now complete. Now, to test it.
> Note: The `spm-test` tool requires root access to build a package(or docker configured in rootless mode).
> If you have incorrectly configured your package, no lasting changes will be made.

Run `spm-test bash.ecmp` inside the package's directory to test it.


