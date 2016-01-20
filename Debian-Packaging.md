Building Tarballs
-----------------

This procedure builds a `conreality-$(VERSION).tar.gz` source tarball for
general distribution:

    $ git clone --recursive https://github.com/conreality/conreality.git /src/conreality
    $ cd /src/conreality
    $ ./autogen.sh
    $ ./configure
    $ make dist          # produces ./conreality-$(VERSION).tar.gz

Building Packages
-----------------

This procedure requires the `conreality-$(VERSION).tar.gz` tarball built
in the previous section and produces Debian binary packages from it:

    $ mkdir -p /tmp/debian
    $ cp conreality-$(VERSION).tar.gz /tmp/debian/
    $ cd /tmp/debian
    $ tar -xf conreality-$(VERSION).tar.gz
    $ mv conreality-$(VERSION).tar.gz conreality_$(VERSION).orig.tar.gz
    $ cd conreality-$(VERSION)
    $ rsync -a /src/conreality/etc/debian/conreality/ debian/
    $ dpkg-buildpackage -us -uc
    $ lintian -i -I --show-overrides

Build Configuration
-------------------

Our Debian packages are built with the following feature configuration:

    $ ./configure --enable-debug --enable-develop --disable-irc

This means that the build host must have the Alcotest and UTop development
packages installed as build dependencies at build time.

Debian Packages
---------------

### OCaml

* `ocaml-base`, `ocaml-base-nox`: `ocamlrun`, `*.cmi`
* `ocaml-interp`: `ocaml` toplevel
* `ocaml-native-compilers`: `ocamlc.opt`, `ocamlopt.opt`, etc.
* `ocaml-nox`: `ocamlc`, `ocamlopt`, `ocamldoc`, `ocamllex`, `ocamlbuild`, etc.
* `ocaml-findlib`: `ocamlfind`

Debian Tooling
--------------

* [`dh_make(8)`](http://manpages.ubuntu.com/manpages/trusty/man8/dh_make.8.html)
* [`dh(1)`](http://manpages.ubuntu.com/manpages/trusty/man1/dh.1.html)
* [`debuild(1)`](http://manpages.ubuntu.com/manpages/trusty/man1/debuild.1.html)
* [`lintian(1)`](http://manpages.ubuntu.com/manpages/trusty/man1/lintian.1.html)
* [`reprepro(?)`](https://mirrorer.alioth.debian.org/reprepro.1.html)

Debian Policy
-------------

* [Debian Packaging Tutorial](https://www.debian.org/doc/manuals/packaging-tutorial/packaging-tutorial.en.pdf)
* [Debian New Maintainers' Guide](https://www.debian.org/doc/manuals/maint-guide/)
* [Debian Policy Manual](https://www.debian.org/doc/debian-policy/)
* [Debian OCaml Packaging Policy](https://pkg-ocaml-maint.alioth.debian.org/ocaml_packaging_policy.html/)
* [Debian OCaml Task Force](https://wiki.debian.org/Teams/OCamlTaskForce)
* https://wiki.debian.org/IntroDebianPackaging
* https://wiki.debian.org/Packaging
* https://wiki.debian.org/HowToPackageForDebian

Ubuntu Policy
-------------

* [Ubuntu Packaging Guide](http://packaging.ubuntu.com/html/)
  * [Basic Overview of the `debian/` Directory](http://packaging.ubuntu.com/html/debian-dir-overview.html)
  * [Packaging New Software](http://packaging.ubuntu.com/html/packaging-new-software.html)
* [The Personal Package Archive (PPA) Guide](https://help.launchpad.net/Packaging/PPA)

Notes on Lintian
----------------

* http://blogs.operationaldynamics.com/pmiller/sw/new-lintian1-changes-distribution-check

Case Examples
-------------

* https://github.com/ocaml/opam/issues/149

See Also
--------

* https://raphaelhertzog.com/2010/09/27/different-dependencies-between-debian-and-ubuntu-but-common-source-package/
* [Arch Linux OCaml package guidelines](https://wiki.archlinux.org/index.php/OCaml_package_guidelines)
* https://forge.ocamlcore.org/tracker/?func=detail&aid=718&group_id=54&atid=291