**NB 1**: This document primarily covers Bitcoin Core as it was in 0.11, although it is occasionally updated to match the latest ("master") Core code. Due to refactors and other code changes, it's possible that some of the functionality mentioned in specific entries was right in 0.11 (or whenever the file was introduced) but isn't now. Corrections are welcomed!

**NB 2**: Unless there are special reasons for listing them, graphics files are left out, although the general outline of what resides in a subdirectory will be discussed.

**NB 3**: Some of these files may not be in the source code downloads for various releases. They should be available in the Core repo on GitHub.

./.appveyor.yml - Provides project-specific info to [AppVeyor](https://www.appveyor.com/), allowing native Windows builds to be created after PRs are created or updated. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13964).

./.gitattributes - Settings that can be specified for a path. *[Used for version info stuff](https://github.com/bitcoin/bitcoin/commit/a20c0d0f6792acf532309eee2e9f29120c801ee4)*.

./.gitignore - File that prevents certain files from showing up in Git.

./.travis.yml - Provides project-specific info to [Travis CI](https://travis-ci.org/), allowing Linux builds and cross-compiled builds (MacOS and Windows) to be created after PRs are created or updated.

./autogen.sh - The first script called in the build process. Does a bit of setup and then calls *autoreconf* to do a proper setup of the autotools build environment.

./configure.ac - *autoconf* input file (and basically the build’s starting point). Sets certain project-related values and describes tests for all features required on the build machine. Run as *./configure* once ./*autogen.sh* has been run.

./COPYING - Copyright info.

./CONTRIBUTING.md - A document explaining some ways in which people can conttribute to the Core project.

./INSTALL.md - Just points you to doc/build-\*.md for build instructions. [*Changed from ./INSTALL to ./INSTALL.md in 0.13.2*](https://github.com/bitcoin/bitcoin/pull/8896).

./libbitcoinconsensus.pc.in - [Used for *pkg-config* support](https://github.com/bitcoin/bitcoin/pull/5334). *pkg-config* allows developers to create .pc files that go alongside libraries (*libbitcoinconsensus* in this case, which is intended to eventually become a standalone library with all the consensus-critical code, separate from the rest of Core). If other programs intend to use the library, the .pc file allows the programs to know which libraries also need to be compiled if the programs are going to use the library in question.

./Makefile.am - *automake* input file. It’s basically the recipe used to create the final Makefile. Run as *./Makefile* once *./autogen.sh* and *./configure* have been run.

./README.md - Base README file.

**./.github** - GitHub-specific materials.

./.github/ISSUE\_TEMPLATE.md - GitHub [issue template](https://github.com/blog/2111-issue-and-pull-request-templates). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8058).

**./.travis** - .travis.yml support scripts. Files added here in part to subject the scripts to *shellcheck*, thereby making them more reliable. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13863). *Files will not be listed.*

**./.tx** - Transifex (i.e., translation) stuff. Used by Qt.

./.tx/config - Transifex config file.

**./build-aux** - Autotools materials. Auxiliary config files (AC\_CONFIG\_AUX\_DIR - configure.ac). *No files actually found here.*

**./build-aux/m4** - Additional local Autoconf macros (AC\_CONFIG\_MACRO\_DIR - configure.ac). Basically tests to see if certain preconditions are met before compiling Core.

./build-aux/m4/ax\_boost\_base.m4 - Checks if Boost C++ libraries meet a particular version.

./build-aux/m4/ax\_boost\_chrono.m4 - Checks for *Chrono* library from Boost.

./build-aux/m4/ax\_boost\_filesystem.m4 - Checks for the *Filesystem* library from Boost.

~~./build-aux/m4/ax\_boost\_program\_options.m4~~ - Checks for the *program\_options* library from Boost. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13482).

./build-aux/m4/ax\_boost\_system.m4 - Checks for the *System* library from Boost.

./build-aux/m4/ax\_boost\_thread.m4 - Checks for the *Thread* library from Boost.

./build-aux/m4/ax\_boost\_unit\_test\_framework.m4 - Checks for unit test framework library from Boost.

./build-aux/m4/ax\_check\_compile\_flag.m4 - Checks whether a given flag works with a compiler.

./build-aux/m4/ax\_check\_link\_flag.m4 - Checks whether a given flag works with a linker.

./build-aux/m4/ax\_check\_preproc\_flag.m4 - Checks whether a given flag works with a language’s preprocessor.

./build-aux/m4/ax\_cxx\_compile\_stdcxx.m4 - Checks whether C++11 or C++14 (Core uses C++11) code can be compiled on a given system. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7165).

./build-aux/m4/ax\_gcc\_func\_attribute.m4 - Checks whether the compiler supports a given GCC function attribute (e.g., "dllimport" or "warn_unused_result").

./build-aux/m4/ax\_pthread.m4 - Determines if pthreads are supported and does some setup work.

./build-aux/m4/bitcoin\_find\_bdb48.m4 - Checks if BerkeleyDB 4.8 is present. [Core-specific](https://github.com/bitcoin/bitcoin/pull/2979).

./build-aux/m4/bitcoin\_qt.m4 - Checks if Qt dependencies are met. [Came about to help make Qt 5 detection more sane](https://github.com/bitcoin/bitcoin/pull/3346).

./build-aux/m4/bitcoin\_subdir\_to\_include.m4 - Used to [indicate the location of BerkeleyDB 4.8 #include files](https://github.com/bitcoin/bitcoin/pull/2979).

./build-aux/m4/l\_atomic.m4 - Checks if *libatomic* is available for std::atomic operations. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8563).

**./build\_msvc** - Files that allow Core to be built using [Microsoft Visual Studio 2017](https://en.wikipedia.org/wiki/Microsoft_Visual_Studio) or later. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/11526). *Unless mentioned below, files will not be discussed here.*

./build\_msvc/msvc-autogen.py - Python script that can auto-generate MSVS project files. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/14062).

**./contrib** - External tools that may be useful but aren’t directly related to Core.

./contrib/bitcoin-qt.pro - [Qt file used by *qmake*](http://doc.qt.io/qt-4.8/qmake-project-files.html) to help compile Qt-related code for Core.

./contrib/bitcoind.bash-completion - [Used to help bash complete *bitcoind* commands](https://github.com/bitcoin/bitcoin/pull/1366)? Looks like it’s activated when doing Debian builds.

./contrib/filter-lcov.py - A Python script that, when combined with *lcov -r* (removes duplicate entries), acts as a significantly faster version of *lcov -r*. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10565).

./contrib/gitian-build.py - Script that simplifies the process of creating a Gitian build. [*Moved from ./contrib/gitian-build.sh in 0.17*](https://github.com/bitcoin/bitcoin/pull/13623).

~~./contrib/gitian-build.sh~~ - Script that simplifies the process of creating a Gitian build. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8566) and [moved to ./contrib/gitian-build.py in 0.17](https://github.com/bitcoin/bitcoin/pull/13623).

./contrib/install\_db4.sh - OpenBSD/UNIX shell script for installing BerkeleyDB 4.8. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11702).

~~./contrib/qt\_translations.py~~ - [Helped OS X include the correct translations](https://github.com/bitcoin/bitcoin/commit/6be6be2ed9d5d4b9dc1657d434a7fed3b3935f6f). [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8781).

./contrib/README.md - Briefly explains many things in the subdirs.

~~./contrib/tidy\_datadir.sh~~ - [Script that cleans up Core datadir](https://github.com/bitcoin/bitcoin/pull/2295) (e.g., wallet.dat, blk00001.dat). Obsolete circa Core 0.7/0.8. [*Removed in 0.17*](https://github.com/bitcoin/bitcoin/pull/13119).

./contrib/valgrind.supp - [Valgrind](https://en.wikipedia.org/wiki/Valgrind) suppression file. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11035).

**./contrib/debian** - Contains files used to package bitcoind/bitcoin-qt for Debian-based Linux systems. *[Added in 0.5](https://github.com/bitcoin/bitcoin/pull/608) [to control PPA builds](https://github.com/bitcoin/bitcoin/pull/600#issuecomment-2631226)*. *[Mostly removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13809) (files moved to [this repo](https://github.com/bitcoin-core/packaging/tree/master/debian)*. All files that were listed here have been removed from this list.

./contrib/debian/copyright - Copyright info file usable by Debian.

~~**./contrib/debian/examples**~~ - Related to Debian packaging. Contains examples for PPA users. *[Removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13809) (files moved to [this repo](https://github.com/bitcoin-core/packaging/tree/master/debian)*.

~~./contrib/debian/examples/bitcoin.conf~~ - Example of a Bitcoin configuration. [*Moved to ./share/examples/bitcoin.conf in 0.17*](https://github.com/bitcoin/bitcoin/pull/13809).

**~~./contrib/debian/manpages~~** - Related to Debian packaging. Package manpages. *Will not discuss individual files.* [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8743).

~~**./contrib/debian/patches**~~ - Related to Debian packaging. [Used by packagers who need to patch Core’s upstream code.](http://packaging.ubuntu.com/html/patches-to-packages.html) *[Removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13809) (files moved to [this repo](https://github.com/bitcoin-core/packaging/tree/master/debian)*. All files that were listed here have been removed from this list.

~~**./contrib/debian/source**~~ - Related to Debian packaging. [Enforces program used to apply packages (Quilt).](http://packaging.ubuntu.com/html/patches-to-packages.html) *[Removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13809) (files moved to [this repo](https://github.com/bitcoin-core/packaging/tree/master/debian)*. All files that were listed here have been removed from this list.

**./contrib/devtools** - Specific tools for devs working on the Core repo.

~~./contrib/devtools/check-doc.py~~ - Checks if all command line args are documented. Used primarily for automated testing by the Core team. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7280) and [moved to ./test/lint/check-doc.py in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/check-rpc-mappings.py~~ - Checks if RPC commands are documented. Used primarily for automated testing by the Core team. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/10751) and [moved to ./test/lint/check-rpc-mappings.py in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

./contrib/devtools/circular-dependencies.py - A script looking for circular dependencies in C++ code. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13228).

./contrib/devtools/clang-format.py - Sets the rules for *clang-format*, a program that formats C/C++/ObjC code. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6790).

./contrib/devtools/clang-format-diff.py - [Formats unified Git diffs according to ./src/.clang-format](http://clang.llvm.org/docs/ClangFormat.html). [Taken from the upstream LLVM repo](https://llvm.org/svn/llvm-project/cfe/trunk/tools/clang-format/clang-format-diff.py). *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7304) and [removed in 0.14](https://github.com/bitcoin/bitcoin/pull/9649)*.

~~./contrib/devtools/commit-script-check.sh~~ - A script that can use commands in a commit to verify that the code pre-commit matches what's in the commit when the commands are executed. Useful for things like mass changes (e.g., removing capitalization in all header files). *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10189) and [moved to ./test/lint/commit-script-check.py in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

./contrib/devtools/copyright\_header.py - Script that does a mass copyright year update. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8674) as a replacement for ./contrib/devtools/fix-copyright-headers.py*.

~~./contrib/devtools/fix-copyright-headers.py~~ - Script that does a mass copyright year update. *[Removed in 0.14](https://github.com/bitcoin/bitcoin/pull/8674) by ./contrib/devtools/copyright\_header.py*.

./contrib/devtools/gen-manpages.sh - A script that's used to generate man pages (located at ./doc/man). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8608)

./contrib/devtools/github-merge.sh - [Used to merge PRs securely and to sign the merge commits.](https://github.com/bitcoin/bitcoin/pull/3302) Used only by those with commit access to the Core repo.

~~./contrib/devtools/git-subtree-check.sh~~ - [Verifies that subtree contents match upstream subtrees.](https://github.com/bitcoin/bitcoin/pull/5965) Must run from repo root. Currently useful for libsecp256k1 and LevelDB. [*Moved to ./test/lint/git-subtree-check.py in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

~~./contrib/devtools/lint-all.sh~~ - Generic shell script that executes all [lint](https://en.wikipedia.org/wiki/Lint_(software)) scripts in ./contrib/devtools. Used primarily for automated testing by the Core team. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11300) and [moved to ./test/lint/lint-all.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-include-guards.sh~~ - A lint script that enforces the usage of [include guards](https://en.wikipedia.org/wiki/Include_guard) in C++ header files. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11300) and [moved to ./test/lint/lint-include-guards.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-includes.sh~~ - A lint script that enforces Core's include guidelines (i.e., no duplicate header includes). *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11300) and [moved to ./test/lint/lint-includes.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-logs.sh~~ - Checks for newline termination in log files. *[Added in 0.17](https://github.com/bitcoin/bitcoin/pull/12891) and [moved to ./test/lint/lint-logs.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-python.sh~~ - A lint script that looks for unused Python imports. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11835) and [moved to ./test/lint/lint-python.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-python-shebang.sh~~ - A lint script that looks for missing Python [shebangs](https://en.wikipedia.org/wiki/Shebang_(Unix)). *[Added in 0.17](https://github.com/bitcoin/bitcoin/pull/12972) and [moved to ./test/lint/lint-python-shebang.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-shell.sh~~ - A lint script that looks for [shellcheck](https://www.shellcheck.net/) warnings in shell scripts (i.e., shell script bugs). *[Added in 0.17](https://github.com/bitcoin/bitcoin/pull/12871) and [moved to ./test/lint/lint-shell.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-tests.sh~~ - A lint script that enforces the naming convention of files in ./src/test/ and ./src/wallet/test/. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11300) and [moved to ./test/lint/lint-test.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

~~./contrib/devtools/lint-whitespace.sh~~ - A lint script that looks for trailing whitespace added by new commits. [*Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11300)* and [moved to ./test/lint/lint-whitespace.sh in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

./contrib/devtools/optimize-pngs.py - [Optimize data in PNG files.](https://github.com/bitcoin/bitcoin/pull/5489)

./contrib/devtools/README.md - Explains everything in the subdir.

./contrib/devtools/security-check.py - Confirms that certain security features (e.g., [PIE](https://en.wikipedia.org/wiki/Position-independent_code#PIE), [NX](https://en.wikipedia.org/wiki/NX_bit), [RELRO](http://tk-blog.blogspot.com/2009/02/relro-not-so-well-known-memory.html), and [canaries](https://en.wikipedia.org/wiki/Stack_buffer_overflow#Stack_canaries)) are used for a given binary. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6854).

./contrib/devtools/split-debug.sh.in - Splits the debug information from a built binary and places it in a separate file. [Used to keep debugging info handy if a stripped binary needs to be debugged](https://sourceware.org/gdb/onlinedocs/gdb/Separate-Debug-Files.html). Autoconfig processes the file and outputs it as ./contrib/devtools/split-debug.sh, which does the actual splitting. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8188).

./contrib/devtools/symbol-check.py - [Makes sure a Linux binary has only gcc, glibc, and libstdc++ version symbols](https://github.com/bitcoin/bitcoin/pull/4089) supported by given versions, thereby maintaining compatibility with minimum supported Linux distro versions.

./contrib/devtools/test-security-check.py - Compiles a simple program in C and confirms that the binary has the security features tested in ./contrib/devtools/security-check.py. [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/6854)

./contrib/devtools/update-translations.py - [Used to fetch new translations from Transifex.](https://github.com/bitcoin/bitcoin/pull/4110)

**./contrib/gitian-descriptors** - Descriptor for *gitian*, the deterministic build system used to create Bitcoin Core binaries for distribution. Describes the VM that will contain the build system and the script that will run on the VM.

./contrib/gitian-descriptors/gitian-linux.yml - Linux (32-bit & 64-bit) descriptor.

./contrib/gitian-descriptors/gitian-osx.yml - OS X (64-bit only) descriptor. Uses an *Xcode* SDK (not available in the repo) to compile the OS X binary under Linux. Code not signed for [Gatekeeper](https://en.wikipedia.org/wiki/Gatekeeper_%28OS_X%29).

./contrib/gitian-descriptors/gitian-osx-signer.yml - [Descriptor that splices in a signature for the final .dmg file.](https://github.com/bitcoin/bitcoin/pull/5363) See ./contrib/macdeploy/ for the signing key tools.

./contrib/gitian-descriptors/gitian-win.yml - Windows (32-bit & 64-bit) descriptor. Uses the *MinGW* development environment to compile the Windows version under Linux. Code not signed for [Windows](https://msdn.microsoft.com/en-us/library/ms537361%28v=vs.85%29.aspx).

./contrib/gitian-descriptors/gitian-win-signer.yml - [Descriptor that splices in a signature for the final .exe file.](https://github.com/bitcoin/bitcoin/pull/6303) [Uses osslsigncode to attach the detached signature to the Core binary.](http://development.adaptris.net/users/lchan/blog/2013/06/07/signing-windows-installers-on-linux/) The tool(s) & steps used to generate the signature don’t appear to be listed in the Core repo.

~~./contrib/gitian-descriptors/README.md~~ - Rough instructions explaining how to do Gitian builds. [*Removed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11414).

**./contrib/gitian-keys** - PGP keys for people who post verifications of Gitian builds. [Moved from /.contrib/gitian-downloader in 0.13.0](https://github.com/bitcoin/bitcoin/pull/7870). In 0.17, the individual key files [were deleted](https://github.com/bitcoin/bitcoin/pull/11909).

./contrib/gitian-keys/keys.txt - List of PGP keys for people who post verifications of Gitian builds. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11909).

./contrib/gitian-keys/README.md - README explaining the basic process.

**./contrib/init** - Sample init scripts and service configuration for *bitcoind*. [Used to assist packagers in creating node packages](https://github.com/bitcoin/bitcoin/pull/4611).

./contrib/init/bitcoind.conf - *Upstart* service configuration file.

./contrib/init/bitcoind.init - CentOS compatible SysV style init script.

./contrib/init/bitcoind.openrc - *OpenRC* compatible SysV style init script.

./contrib/init/bitcoind.openrcconf - *OpenRC* conf.d file.

./contrib/init/bitcoind.service - *systemd* service unit configuration. Useful for things like hardening `bitcoind` by limiting the ability of the binary to gain new, unintended privileges.

./contrib/init/org.bitcoin.bitcoind.plist - [Launch agent](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html) that OS X can use to launch *bitcoind* at startup. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6621).

./contrib/init/README.md - Mostly a short version of doc/init.md.

**./contrib/linearize** - Construct a linear, no-fork, best version of the blockchain. Was originally one script, and now split into two scripts. *[Added in 0.9](https://github.com/bitcoin/bitcoin/commit/701f6c35bc493739eb0acc97da828c992772cbeb)*.

./contrib/linearize/example-linearize.cfg - Example of a config to use for both linearization steps. No specific directions for config development seem to exist.

./contrib/linearize/linearize.py - The original linearization script. *[Added in 0.9](https://github.com/bitcoin/bitcoin/commit/701f6c35bc493739eb0acc97da828c992772cbeb) under a different name, then [moved to ./contrib/linearize/linearize-hashes.py in 0.10](https://github.com/bitcoin/bitcoin/pull/4757)*.

./contrib/linearize/linearize-data.py - Step 2 in linearization. Takes the list of incoming block hashes and generates a full, in-order blockchain in one output file. *[Added in 0.10](https://github.com/bitcoin/bitcoin/pull/4757)*.

./contrib/linearize/linearize-hashes.py - Step 1 in linearization. Uses the *getblockhash* RPC call to get all the block hashes from block X to block Y and print them to the command line. *[Moved from ./contrib/linearize/linearize.py in 0.10](https://github.com/bitcoin/bitcoin/pull/4757)*.

./contrib/linearize/README.md - Explains how to use everything.

**./contrib/macdeploy** - [Used to create a .dmg package for Bitcoin Core.](https://github.com/bitcoin/bitcoin/commit/6eaa1b36fcf5a3b28c2440a3cf8ab4780f1afef9) [Uses a detached signature repo so that anybody can grab the appropriate sigs.](https://github.com/bitcoin/bitcoin/pull/6269) (Cory Fields/"theuni" is the only person who can actually generate the sigs, which he then uploads to the [sig repo](https://github.com/bitcoin/bitcoin-detached-sigs).) Used to make Core compatible with Apple’s "Gatekeeper" scheme. *Graphics files have been removed from this listing.*

./contrib/macdeploy/custom\_dsstore.py - Creates a custom .DS\_Store file added to DMG files that deploy Bitcoin Core software to end users. (The file allows for background images and other features.) *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7192)*.

./contrib/macdeploy/detached-sig-apply.sh - Applies a detached signature from a repo and attached the signature to an unsigned OS X build to create a signed build. ./contrib/gitian-descriptors/gitian-osx-signer.yml contains a usage example.

./contrib/macdeploy/detached-sig-create.sh - Creates a detached signature of an OS X build that can then be uploaded to a repo for downloading and attachment via the ./contrib/macdeploy/detached-sig-apply.sh script that [basically uses *codesign* to create a detached signature covering Core’s entire .app directory](http://blog.erickdransch.com/2012/02/signing-mac-builds/). To be used only by somebody with the Apple-supplied signing key.

./contrib/macdeploy/DS\_Store - Apple-specific binary file. [Used for packaging purposes.](https://github.com/bitcoin/bitcoin/pull/3885)

./contrib/macdeploy/extract-osx-sdk.sh - Shell script used to extract the OS X SDK from [*Xcode*](https://en.wikipedia.org/wiki/Xcode). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8617).

./contrib/macdeploy/fancy.plist - Used to generate a "fancy" DMG disk image (i.e., the screen that allows the user, when a DMG file is double-clicked, to install Core).

./contrib/macdeploy/LICENSE - GNUv3 license.

./contrib/macdeploy/macdeployqtplus - The Python script that’s used to assemble everything into an OS X-friendly app format (i.e., the .app directory) and place it in a .dmg file that's ready for distribution.

./contrib/macdeploy/README.md - Deployment instructions. Presumably up-to-date.

**./contrib/macdeploy/Base.lproj** - [Required for app bundle name purposes.](https://developer.apple.com/library/ios/documentation/MacOSX/Conceptual/BPInternational/MaintaingYourOwnStringsFiles/MaintaingYourOwnStringsFiles.html) [Used to avoid a hack.](https://github.com/bitcoin/bitcoin/pull/6214#issuecomment-107962813)

./contrib/macdeploy/Base.lproj/InfoPlist.strings - Contains strings needed by the app bundle. Can be split up according to language but isn’t (for now?).

**./contrib/qos** - [Script that can limit bandwidth used by Core.](https://github.com/bitcoin/bitcoin/pull/2728)

./contrib/qos/README.md - Explains the QOS script.

./contrib/qos/tc.sh - Script that uses *tc* to limit the bandwidth.

~~**./contrib/rpm**~~ - Spec files for generating [RPM packages](https://en.wikipedia.org/wiki/RPM_Package_Manager). *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7609) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13809) (files moved to [this repo](https://github.com/bitcoin-core/packaging/tree/master/rpm)*. All files that were listed here have been removed from this list.

**./contrib/seeds** - [Generates a list of fixed seed nodes.](https://github.com/bitcoin/bitcoin/commit/9126e08739f5115c3032997cabd23f27037131ef) Nodes are then used to update ./src/chainparamsseeds.h

./contrib/seeds/generate-seeds.py - Script used to generate ./src/chainparamsseeds.h.

./contrib/seeds/makeseeds.py - Parses data from Pieter Wuille’s website. Presumably pulls down nodes for nodes\_main.txt.

./contrib/seeds/nodes\_main.txt - List of mainnet nodes (IPv4, IPv6, and Onion). Tied to generate-seeds.py.

./contrib/seeds/nodes\_test.txt - [List of testnet nodes](https://github.com/bitcoin/bitcoin/pull/6333) (Onion-only). Tied to generate-seeds.py.

./contrib/seeds/README.md - Gives a bit of context to the tool.

**~~./contrib/spendfrom~~** - [Use the raw transactions API to send coins received on a particular address (or addresses).](https://github.com/bitcoin/bitcoin/pull/2162) [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8779).

~~./contrib/spendfrom/README.md~~ - Explains how to use the script.

~~./contrib/spendfrom/setup.py~~ - Standard Python setup.py file.

~~./contrib/spendfrom/spendfrom.py~~ - The script to run.

**./contrib/testgen** - [Utilities to generate test vectors for the data-driven Bitcoin tests.](https://github.com/bitcoin/bitcoin/pull/1888)

./contrib/testgen/base58.py - Support script for Base58 encode/decode.

./contrib/testgen/gen\_base58_test\_vectors.py - The script to run. [*Removed in 0.18*](https://github.com/bitcoin/bitcoin/pull/13935).

./contrib/testgen/gen\_key\_io_test\_vectors.py - The script to run. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13935).

./contrib/testgen/README.md - Shows how to run the script but doesn’t explain what it all means.

**./contrib/verify-commits** - [Git tool to verify that every merge commit was signed by a trusted key using ./contrib/devtools/github-merge.sh](https://github.com/bitcoin/bitcoin/pull/5149), along with forcing PGP-signed commits. It’s meant only for those with commit access.

./contrib/verify-commits/allow-incorrect-sha512-commits - Whitelisted commits that cause errors when checking Core's SHA-512 commit tree. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13066).

./contrib/verify-commits/allow-revsig-commits - Whitelisted commits signed by a revoked key. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6875).

./contrib/verify-commits/allow-unclean-merge-commits - Whitelisted commits that had unclean merges. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13066).

./contrib/verify-commits/gpg.sh - The "gpg.program" Git variable is set to this script, which will [act as a *GnuPG* substitute](https://git-scm.com/docs/git-config). Used instead of *GnuPG* to do the actual signature verification.

./contrib/verify-commits/pre-push-hook.sh - [If copied to .git/hooks/pre-push (and BASH is installed)](https://github.com/bitcoin/bitcoin/pull/5149#issuecomment-67726007), this script prevents the pushing of unsigned commits to *master* on bitcoin/bitcoin. Git info [here](https://git-scm.com/docs/githooks).

./contrib/verify-commits/README.md - README explaining the purpose of the tool and how to use it safely. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7713).

./contrib/verify-commits/trusted-git-root - The point at which the commit tree stops looking to confirm that the code is accurate. Everything before this commit is assumed to be safe.

./contrib/verify-commits/trusted-keys - Fingerprints of trusted keys used to push commits. Used when going through commits to ensure that all signatures come from keys that are trusted.

./contrib/verify-commits/trusted-sha512-root-commit - The point at which the commit tree stops looking to confirm that the code is accurate. Everything before this commit is assumed to be safe. "Tree-SHA512" is only in merge commits, and is the [SHA512 hash of the resulting merged tree](https://github.com/bitcoin/bitcoin/pull/9871). [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9880).

./contrib/verify-commits/verify-commits.py - Called by ./contrib/verify-commits/pre-push-hook.sh. Verifies that the commits before the current one have been properly signed, and that the commit about to be pushed has been signed by an accepted key. [*Replaced ./contrib/verify-commits/verify-commits.sh in 0.17*](https://github.com/bitcoin/bitcoin/pull/13066).

~~./contrib/verify-commits/verify-commits.sh~~ - Called by ./contrib/verify-commits/pre-push-hook.sh. Verifies that the commits before the current one have been properly signed, and that the commit about to be pushed has been signed by an accepted key. [*Replaced by ./contrib/verify-commits/verify-commits.py in 0.17*](https://github.com/bitcoin/bitcoin/pull/13066).

**./contrib/verifybinaries** - [Script that verifies binaries downloaded from bitcoin.org](https://github.com/bitcoin/bitcoin/pull/1935) [and bitcoincore.org](https://github.com/bitcoin/bitcoin/pull/10651). [*Moved from ./contrib/verifysfbinaries in 0.13*](https://github.com/bitcoin/bitcoin/pull/7881).

./contrib/verifybinaries/README.md - Basically explains what’s going on.

./contrib/verifybinaries/verify.sh - The verification script.

**./contrib/zmq** - Support for ØMQ (ZeroMQ), an asynchronous messaging library. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6103).

./contrib/verifysfbinaries/zmq\_sub.py - Working example of adding ØMQ support. [*Requires Python 3.5 or higher as of 0.15*](https://github.com/bitcoin/bitcoin/pull/6103).

./contrib/verifysfbinaries/zmq\_sub3.4.py - Working example of adding ØMQ support using Python 3.4. Basically the same as ./contrib/verifysfbinaries/zmq\_sub.py, with the only difference being in how the [*asyncio*](https://docs.python.org/3/library/asyncio.html) library is used. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9485).

**./depends** - A shared dependency builder. See AC\_CONFIG\_AUX\_DIR() in ./configure.ac to see how Autotools connects to these files. [*Added in 0.10*](https://github.com/bitcoin/bitcoin/pull/4592).

./depends/.gitignore - Lists files for Git to ignore.

./depends/config.guess - [Used by *Autoconf* to guess a canonical system name.](http://www.gnu.org/savannah-checkouts/gnu/autoconf/manual/autoconf-2.69/html_node/Specifying-Target-Triplets.html)

./depends/config.site.in - Defines some variables. ./depends/Makefile processes the file and uses it to output ./depends/config.site, which causes the build to [override some build settings on the building machine.](http://www.gnu.org/software/automake/manual/html_node/config_002esite.html#config_002esite)

./depends/config.sub - [Used by *Autoconf* to convert system aliases into full canonical names.](http://www.gnu.org/savannah-checkouts/gnu/autoconf/manual/autoconf-2.69/html_node/Specifying-Target-Triplets.html)

./depends/description.md - General description of the depends system. Some high-level technical details of the depends setup.

./depends/funcs.mk - Various functions and variables related to building the dependencies in the ./depends/packages subdirectory.

./depends/Makefile - Root makefile for shared dependency building.

./depends/packages.md - Steps for adding packages. Low-level "recipe" details. Good for devs.

./depends/README.md - Some general details and *make* options and such.

**./depends/builders** - [Shared dependency builder.](https://github.com/bitcoin/bitcoin/pull/4592) Compiler/Linker variables and such required by the machine building the binary. (The "builder" identity is automated and determined by ./config.guess.) Used by ./depends/Makefile.

./depends/builders/darwin.mk - Overriding values for OS X building systems.

./depends/builders/default.mk - Default values for all builders. Called by ./depends/Makefile, along with the appropriate builder-specific .mk file.

./depends/builders/linux.mk - Overriding values for Linux building systems.

**./depends/hosts** - [Shared dependency builder.](https://github.com/bitcoin/bitcoin/pull/4592) Compiler/Linker variables and such required to build for the host machine (i.e., the machine that’ll run the final binary). The host may be specified, otherwise it’ll default to the builder. Used by ./depends/Makefile.

./depends/hosts/darwin.mk - Overriding OS X build variable values.

./depends/hosts/default.mk - Default build variable values. Called by ./depends/Makefile, along with the appropriate host-specific .mk file.

./depends/hosts/linux.mk - Overriding Linux build variable values.

./depends/hosts/mingw32.mk - Overriding Windows (MinGW) build variable values.

**./depends/packages** - Info on packages to download and compile as Core dependencies. Almost all the packages are actually required only by Qt 4 or 5. Native packages are used to build towards particular host/target platforms when the host requires tools not directly found on the native (i.e., build) platform, so the native platform must use alternate tools.

./depends/packages/bdb.mk - BerkeleyDB 4.8. Used by all versions of the Bitcoin Core wallet.

./depends/packages/boost.mk - Boost. Used by all versions of Core, including for consensus-critical functionality.

./depends/packages/dbus.mk - D-Bus. Used by Qt.

./depends/packages/expat.mk - Expat (XML parser). Used by Qt.

./depends/packages/fontconfig.mk - Fontconfig. Used by Qt.

./depends/packages/freetype.mk - FreeType. Used by Qt.

./depends/packages/libevent.mk - *libevent* (event notification) library. Used by all versions of Core.

~~./depends/packages/libICE.mk~~ - Inter-Client Exchange (ICE) library. Used by Qt 4. [*Removed in 0.18*](https://github.com/bitcoin/bitcoin/pull/14183).

~~./depends/packages/libSM.mk~~ - Session Management library (SMlib). Used by Qt 4. [*Removed in 0.18*](https://github.com/bitcoin/bitcoin/pull/14183).

./depends/packages/libX11.mk - X11 library. Used by Qt.

./depends/packages/libXau.mk - X11 Authorization Protocol library. Used by Qt.

./depends/packages/libxcb.mk - X protocol C-language Binding (XCB) library. Used by Qt.

./depends/packages/libXext.mk - X Record Extension library. Used by Qt.

./depends/packages/miniupnpc.mk - MiniUPnP. Used by all versions of the [UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play) feature of Core.

~~./depends/packages/native\_biplist.mk~~ - Python binary property list ([plist](https://en.wikipedia.org/wiki/Property_list)) read/write library (native). Used for the OS X build. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7192) to make software name consistency easier and  [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/12625)*.

~~./depends/packages/native\_ccache.mk~~ - [C/C++ compiler cache](https://ccache.samba.org/) (native). [*Removed in 0.17*](https://github.com/bitcoin/bitcoin/pull/12607).

./depends/packages/native\_cctools.mk - [Apple (cctools) toolchain for Linux](https://code.google.com/p/ios-toolchain-based-on-clang-for-linux/) (native). Contains the code used to build the binaries needed to create Apple binaries (e.g., *dyld*, *ld64*, etc.). [Needed to link binaries in an Apple-friendly manner](http://www.ninthavenue.com.au/how-to-build-an-ios-toolchain-for-linux-debian-7).

./depends/packages/native\_cdrkit.mk - [*cdrkit* toolkit](https://en.wikipedia.org/wiki/Cdrkit) (native). The *genisoimage* tool is used to create DMG files used for Apple builds.

~~./depends/packages/native\_comparisontool.mk~~ - A [snapshot](https://github.com/theuni/bitcoind-comparisontool) of the [*pull-tests*](https://github.com/TheBlueMatt/test-scripts) code that was eventually merged into to the *bitcoinj* library (native). (*bitcoinj* now contains [the latest version](https://github.com/bitcoinj/bitcoinj/blob/master/core/src/test/java/org/bitcoinj/core/BitcoindComparisonTool.java) but this package doesn't use the latest version for unknown reasons.) Can be used with the *--with-comparison-tool* and *--enable-tests* configuration options to set the Java comparison tool required by ./qa/pull-tester/run-bitcoind-for-test.sh. *[Removed in 0.14](https://github.com/bitcoin/bitcoin/pull/8504) when support for the Java comparison tool was removed*.

./depends/packages/native\_ds\_store.mk - Python [.DS_Store](https://en.wikipedia.org/wiki/.DS_Store) read/write library (native). Used for the OS X build. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7192).

./depends/packages/native\_libdmg-hfsplus.mk - HFS+/DMG manipulation libraries (native). The *dmg* tool is used to compress DMG files used for OS X builds.

./depends/packages/native\_mac\_alias.mk - Python [Alias](https://en.wikipedia.org/wiki/Alias_%28Mac_OS%29) read/write library (native). Used for the OS X build. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7192).

./depends/packages/native\_protobuf.mk - [Protocol Buffers](https://en.wikipedia.org/wiki/Protocol_Buffers) library (native). Used by Qt as part of BIP 70 support.

./depends/packages/openssl.mk - [OpenSSL](https://www.openssl.org/) library. Provides some cryptographic functionality. Used by all versions of Core, [primarily to support BIP 70](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-January/015490.html). Used to be part of consensus-critical functionality, all of which has since been changed to use *libsecp256k1*.

./depends/packages/packages.mk - Package variables. Specifies the packages requried by various platforms, including packages required by Qt.

./depends/packages/protobuf.mk - [Protocol Buffers](https://en.wikipedia.org/wiki/Protocol_Buffers) variables. Used by Qt as part of BIP 70 support.

./depends/packages/qrencode.mk - [libqrencode](https://fukuchi.org/works/qrencode/) variables. Used by Qt.

./depends/packages/qt.mk - Qt 5 variables.

~~./depends/packages/qt46.mk~~ - Qt 4.6 variables. *[Removed in 0.14](https://github.com/bitcoin/bitcoin/pull/8640), although support for Qt 4 was removed in an earlier version (0.13?)*.

./depends/packages/rapidcheck.mk - [rapidcheck](https://github.com/emil-e/rapidcheck) variables. Used for [property-based testing](https://en.wikipedia.org/wiki/QuickCheck). [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12775).

./depends/packages/xcb\_proto.mk - [XML-XCB protocol description bindings](https://xcb.freedesktop.org/XmlXcb/). Used by Qt.

./depends/packages/xextproto.mk - [X protocol extensions](https://community.linuxmint.com/software/view/libxext6) library. Used by Qt.

./depends/packages/xproto.mk - [X window system core protocol](http://www.x.org/releases/X11R7.7/doc/xproto/x11protocol.html) library. Used by Qt.

./depends/packages/xtrans.mk - [xtrans](http://www.x.org/releases/X11R7.7/doc/xtrans/xtrans.html) library. Used by Qt.

./depends/packages/zlib.mk - [zlib](http://www.zlib.net/). Used by all versions of Core built for Qt 5.7 and beyond. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9646).

./depends/packages/zmq.mk - [ØMQ](http://zeromq.org/) (aka ZeroMQ). Used by all versions of Core.

**./depends/patches** - Patches to be applied to downloaded packages before building the packages. *Nothing in the root directory.*

**./depends/patches/biplist** - [*biplist*](https://bitbucket.org/wooster/biplist) patches. *Added in 0.13 via a direct commit to the 0.13 branch, and not a pull request. See [here](https://github.com/bitcoin/bitcoin/pull/8373) for the master commit*.

./depends/patches/biplist/sorted\_list.patch - Patch that makes the *biplist* output in the .DS\_Store file of OSX DMG files deterministic. *Added in 0.13 via a direct commit to the 0.13 branch, and not a pull request. See [here](https://github.com/bitcoin/bitcoin/pull/8373) for the master commit*.

**./depends/patches/boost** - [*Boost*](http://www.boost.org/) patches.

./depends/patches/boost/fix-win-wake-from-sleep.patch - Upstream Boost patch that fixes a "wake from sleep" issue on Windows. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8899).

**~~./depends/patches/libevent~~** - *libevent* patches. [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/9471).

~~./depends/patches/libevent/libevent-2-fixes.patch~~ - Fixes an issue when compiling with *mingw-w64* on Ubuntu 15.10 and beyond. *[Added for intended use in 0.14](https://github.com/bitcoin/bitcoin/pull/8730) but [removed before the final release](https://github.com/bitcoin/bitcoin/pull/9471)*.

~~./depends/patches/libevent/reuseaddr.patch~~ - [Fixes a Windows socket issue.](https://github.com/bitcoin/bitcoin/pull/5677#issuecomment-135918349) *[Added in 0.12](https://github.com/bitcoin/bitcoin/pull/5677) and [removed in 0.14](https://github.com/bitcoin/bitcoin/pull/9471)*.

**./depends/patches/native\_cdrkit** - cdrkit patches.

./depends/patches/native\_cdrkit/cdrkit-deterministic.patch - [Makes *cdrkit* deterministic](https://github.com/bitcoin/bitcoin/pull/4592).

**~~./depends/patches/native\_mac\_alias~~** - Alias (Python) patches. [*Removed in 0.17*](https://github.com/bitcoin/bitcoin/pull/12417).

~~./depends/patches/native\_mac\_alias/python3.patch~~ - Makes *Alias* Python3 compatible. [*Removed in 0.17*](https://github.com/bitcoin/bitcoin/pull/12417).

**./depends/patches/qt** - Qt 5 patches.

~~./depends/patches/qt/configure-xcoderun.patch~~ - Allows *Qt* compilation (using the *depends* system) to occur when using *Xcode 8*. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8820) but [removed before the final release](https://github.com/bitcoin/bitcoin/pull/9469)*.

~~./depends/patches/qt/fix-cocoahelpers-macos.patch~~ - Fixes a `make depends` build error for Qt. *[Added in 0.16.1](https://github.com/bitcoin/bitcoin/pull/12636) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/12971)*.

~~./depends/patches/qt/fix-xcb-include-order.patch~~ - Fixes various compile errors for *libxcb*. [*Removed in 0.17*](https://github.com/bitcoin/bitcoin/pull/12971).

./depends/patches/qt/fix\_configure\_mac.patch - Updates the Mac config module for Qt 5.9.4. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12971).

./depends/patches/qt/fix\_no\_printer.patch - Fixes the print module for Qt 5.9.4. Required due to Mac issues. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12971).

./depends/patches/qt/fix\_qt\_pkgconfig.patch - Mods a [Qt feature file](http://doc.qt.io/qt-5/qmake-project-files.html) such that [*pkg-config*](http://pkg-config.freedesktop.org/) support continues to be enabled. Undoes a Qt [commit](https://github.com/qtproject/qtbase/commit/6c5d227da1709eb81968823f38a133747c0e95b0) that disabled .pc files for Qt frameworks and internal modules. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8210).

./depends/patches/qt/fix\_riscv64\_arch.patch - Fixes a compilation issue for 64-bit [RISC](https://en.wikipedia.org/wiki/Reduced_instruction_set_computer) processors in Qt 5.9.4. Used to enable Qt `depends` support for 64-bit RISC processors. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13665).

./depends/patches/qt/mac-qmake.conf - *qmake* config variables and such.

~~./depends/patches/qt/mingw-uuidof.patch~~ - Required to build with MinGW. *[Added in 0.12](https://github.com/bitcoin/bitcoin/pull/6471) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/12971)*.

~~./depends/patches/qt/pidlist\_absolute.patch~~ - Fixes Qt "PIDLIST\_ABSOLUTE" issue. *[Added in 0.12](https://github.com/bitcoin/bitcoin/commit/0b416c6e9c3f9f81bea16168f82af77f4e8724bb) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/12971)*.

~~./depends/patches/qt/qfixed-coretext.patch~~ - Allows *Qt* compilation (using the *depends* system) to occur when using *Xcode 9.3*. *[Added in 0.16.1](https://github.com/bitcoin/bitcoin/pull/12946) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/12971)*.

~~./depends/patches/qt/qfixed-coretext.patch~~ - Allows *Qt* compilation (using the *depends* system) to occur when using *Xcode 9.3*. *[Added in 0.16.1](https://github.com/bitcoin/bitcoin/pull/12946) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/12971)*.

./depends/patches/qt/xkb-default.patch~~ - A temporary fix for a determinism build issue that was introduced by Qt 5.8. *[Added in 0.17](https://github.com/bitcoin/bitcoin/pull/14000)*.

~~**./depends/patches/qt46**~~ - Qt 4.6 patches. [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8645).

~~./depends/patches/qt46/stlfix.patch~~ - [Fixes compile issue under Qt 4.6.](https://github.com/bitcoin/bitcoin/commit/0b416c6e9c3f9f81bea16168f82af77f4e8724bb)[*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8645).

**./depends/patches/zeromq** - ØMQ patches. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8238).

./depends/patches/zeromq/0001-fix-build-with-older-mingw64.patch - Patch fixing an issue with builds from pre-4.0 MinGW builds. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/9254).

./depends/patches/zeromq/0002-disable-pthread-set-name-np.patch - Disables ØMQ's usage of *pthread_setname_np()*, a call that [can't be checked by ./contrib/devtools/symbol-check.py due to a lack of *glibc* support](https://github.com/bitcoin/bitcoin/pull/11986#issuecomment-367779254). [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11986).

~~./depends/patches/zeromq/9114d3957725acd34aa8b8d011585812f3369411.patch~~ - Upstream patch that enables MinGW static linking. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8238) and [removed in 0.16](https://github.com/bitcoin/bitcoin/pull/9254).

~~./depends/patches/zeromq/9e6745c12e0b100cd38acecc16ce7db02905e27c.patch~~ - Upstream patch that fixes an issue with MinGW static linking. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8238) and [removed in 0.16](https://github.com/bitcoin/bitcoin/pull/9254).

**./doc** - Various documents. *Graphics and some docs not included in official releases are not mentioned. To see the doc contents, look in ./doc/release-notes.md in official releases.*

./doc/.gitignore - File that prevents certain files from showing up in Git. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10166).

./doc/assets-attribution.md - Graphics attributions. Nothing special.

./doc/benchmarking.md - Describes what the system benchmarks, some things that still need to be benchmarked, and directions for running the benchmarks. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8110).

./doc/bips.md - List of BIPs implemented by Core, the version where they were added, the PR #, and, if relevant, the block where the BIP was activated.

./doc/build-freebsd.md - Details regarding building under FreeBSD. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13372).

./doc/build-netbsd.md - Details regarding building under NetBSD. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/12294).

./doc/build-openbsd.md - Details regarding building under OpenBSD.

./doc/build-osx.md - Details regarding regular (non-Gitian) OSX builds.

./doc/build-unix.md - General (non-Gitian) build notes for Linux.

./doc/build-windows.md - General (non-Gitian) build notes for cross-compiling the Windows (MinGW) build.

./doc/dependencies.md - Provides information on the dependencies required by Core. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/10779).

./doc/descriptors.md - Provides info on the [output descriptors](https://gist.github.com/sipa/e3d23d498c430bb601c5bca83523fa82) used in Core. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/14076).

./doc/developer-notes.md - General dev notes. Lots of miscellaneous things.

./doc/dnsseed-policy.md - [Details regarding DNS seeds.](https://github.com/bitcoin/bitcoin/pull/4566) Explains the rules regarding running a DNS seed. The seed will become a CDNSSeedData entry [as added in ./src/chainparams.cpp](https://github.com/bitcoin/bitcoin/blob/550d4fa7a77c9763d4de9e0c0c48bc2655a65017/src/chainparams.cpp#L97-L102).

./doc/Doxyfile.in - Doxygen (documentation system) config file. Defines certain variables lused throughout Core related to names (*PACKAGE\_NAME*), Core version (*PACKAGE\_VERSION*), etc. [*Moved from ./doc/Doxyfile in 0.15*](https://github.com/bitcoin/bitcoin/pull/10155).

./doc/files.md - Explains which files are made by Core (e.g., blockchain files).

./doc/fuzzing.md - Explains how to use the *test\_bitcoin\_fuzzy* fuzzing harness in ./src/test/test\_bitcoin\_fuzzy.cpp via [AFL](http://lcamtuf.coredump.cx/afl/). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9172).

./doc/gitian-building.md - Details regarding Gitian building. *[As of 0.16](https://github.com/bitcoin/bitcoin/pull/11401), all this says is that the doc has been moved to [Core's document repo](https://github.com/bitcoin-core/docs/blob/master/gitian-building.md).*

./doc/init.md - "Sample init scripts and service configuration for bitcoind".

./doc/multiwallet-qt.md - "Multiwallet Qt Development and Integration Strategy". *Old document that was [removed in 0.14](https://github.com/bitcoin/bitcoin/pull/8879)*.

./doc/psbt.md - Explains Partially Signed Bitcoin Transactions and how to use/create them. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13941).

./doc/README.md - General catch-all / index of sorts.

./doc/README\_osx.md - Details regarding on the deterministic build. [*Changed from .txt to .md in 0.13*](https://github.com/bitcoin/bitcoin/pull/8229).

./doc/README\_windows.txt - Vague Windows README. Not much useful info.

./doc/reduce-traffic.md - Ways to reduce traffic on an Internet connection when running Core.

./doc/release-notes.md - Release notes for the latest version.

./doc/release-process.md - Steps for putting out new releases.

./doc/REST-interface.md - Details regarding using the REST interface ("-test" option).

./doc/shared-libraries.md - Discusses shared libraries created and used by Core (e.g., *bitcoinconsensus*).

./doc/tor.md - Details regarding Tor support in Core.

./doc/translation\_process.md - More translation notes.

./doc/translation\_strings\_policy.md - Details on how the translation system works.

./doc/travis-ci.md - Details regarding the Travis CI testing system. [*Changed from .txt to .md in 0.14*](https://github.com/bitcoin/bitcoin/pull/8879).

~~./doc/unit-tests.md~~ - Details regarding running and adding unit tests. *[Removed in 0.14](https://github.com/bitcoin/bitcoin/pull/9065) and placed inside ./src/test/README.md*.

./doc/zmq.md - Details regarding using ØMQ.

**~~./doc/gitian-building~~** - Graphics used in Gitian guide. *Will not list the files. [Removed in 0.16](https://github.com/bitcoin/bitcoin/pull/11401)*.

**./doc/man** - *man* pages that, as of 0.14, are installed by default when running *make install* during the build process.

./doc/man/bitcoin-cli.1 - The *man* page for the *bitcoin-cli* binary. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8608)

./doc/man/bitcoin-qt.1 - The *man* page for the *bitcoin-qt* binary. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8608)

./doc/man/bitcoin-tx.1 - The *man* page for the *bitcoin-tx* binary. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8608)

./doc/man/bitcoind.1 - The *man* page for the *bitcoind* binary. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8608)

./doc/man/Makefile.am - The Makefile that's used to instal the *man* pages. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8608)

**./doc/release-notes** - Release note archive. *Will not list the files.*

**~~./qa~~** - Core and related tests. Deals primarily with the Core binaries and how they respond to external input (flags, messages, etc.), not tests for internal source code. [*Moved to ./test in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956) along with all subdirectories, with only a couple of files/subdirectories listed below for historical purposes.

**~~./qa/pull-tester~~** - A set of tools that can be used to kick off Python-based tests, primarily based on Core's RPC functionality but including other test types based on external functionality. [*Moved to ./test/functional in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956), with only a couple of files listed below for historical purposes.

~~./qa/pull-tester/run-bitcoind-for-test.sh.in~~ - Runs an instance of *bitcoind* in regtest mode. AC\_CONFIG\_FILES() (./configure.ac) processes the file and outputs it as ./qa/pull-tester/run-bitcoind-for-test.sh, which does the actual running of *bitcoind*. ./Makefile.am shows how to run the script, which is done when executing *make check* during the build process. Requires a "pull-tests" JAR file, which can come from [compiling *bitcoinj*](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2014-August/006407.html) or [downloading the pre-compiled JAR file in depends/packages/native\_comparisontool.mk](https://github.com/theuni/bitcoind-comparisontool). The Java tools run the same tests using *bitcoinj* and compare the results with those from the original *bitcoind* binary run. Can be run with or without "expensive" reorg tests (the "--enable-comparison-tool-reorg-tests" flag when configuring the Core build). Look [here](https://github.com/TheBlueMatt/test-scripts) to see where the test was developed and where the data driving the tests originated. [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/9276).

~~./qa/pull-tester/tests\_config.ini.in~~ - Sets, via Autoconfig wizardry, some variables to be used in ./qa/pull-tester/rpc-tests.ini, which is read by Python's *ConfigParser* module. Examples include enabling ØMQ tests. [*Moved from ./qa/pull-tester/tests\_config.py.in in 0.15*](https://github.com/bitcoin/bitcoin/pull/9657), and [*moved to ./test/functional in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

~~./qa/pull-tester/tests\_config.py.in~~ - Sets, via Autoconfig wizardry, some variables to be used in ./qa/pull-tester/rpc-tests.py. Examples include enabling ØMQ tests. [*Moved to ./qa/pull-tester/tests\_config.ini.in in 0.15*](https://github.com/bitcoin/bitcoin/pull/9657).

**./share** - External materials used by Core one way or another but not part of the source code.

./share/genbuild.sh - [Used to generate build info (and ./src/build.h).](https://github.com/bitcoin/bitcoin/pull/1054)

./share/setup.nsi.in - [Autotools stuff.](https://github.com/bitcoin/bitcoin/pull/2943) Autoconfig will process it and output it as ./share/setup.nsi, which is a [Windows setup file.](https://en.wikipedia.org/wiki/Nullsoft_Scriptable_Install_System)

**./share/examples** - Exmaples of user-configurable Core-related files. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13809).

./share/examples/bitcoin.conf - Example of a Bitcoin configuration. [*Moved from ./contrib/debian/examples/bitcoin.conf in 0.17*](https://github.com/bitcoin/bitcoin/pull/13809).

**./share/rpcauth** - Helps create multi-user RPC login credentials. *[Added as ./src/rpcauth in 0.12](https://github.com/bitcoin/bitcoin/pull/7044) and [moved from there in 0.16](https://github.com/bitcoin/bitcoin/pull/11836)*.

./share/rpcauth/README.md - General README for ./share/rpcuser/rpcuser.py.

./share/rpcauth/rpcauth.py - Creates multi-user RPC login credentials. [*Moved from ./share/rpcuser/rpcuser.py in 0.16*](https://github.com/bitcoin/bitcoin/pull/11836).

**.~~/share/certs*~~* - Certificate materials used to sign Core binaries. [*Removed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11380).

~~./share/certs/BitcoinFoundation\_Apple\_Cert.pem~~ - [Code-signing cert from Apple (OS X).](https://github.com/bitcoin/bitcoin/pull/2179)

~~./share/certs/BitcoinFoundation\_Comodo\_Cert.pem~~ - [Code-signing cert from Comodo (Windows).](https://github.com/bitcoin/bitcoin/pull/2179)

./share/certs/PrivateKeyNotes.md - Code signing threat analysis.

**./share/pixmaps** - Graphics/Icons used outside the Qt framework. *Files not listed.*

**./share/qt** - Materials related to Qt but not directly used by Core.

./share/qt/extract\_strings\_qt.py - [Converts certain strings into Qt 4-friendly strings if needed.](https://github.com/bitcoin/bitcoin/pull/521)

./share/qt/Info.plist.in - OS X bundle kickoff file. Processed by Autoconfig to generate ./share/qt/Info.plist, which is included in the root of the OS X build.

~~./share/qt/protobuf.pri~~ - *qmake* file integrating Payment Protocol (BIP 70) with *protoc*. [Required OpenSSL & Qt.](https://github.com/bitcoin/bitcoin/pull/2539). [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8783).

**./src** - The subdirectory with all the Core-specific code.

./src/.clang-format - Sets the rules for *clang-format*, a program that formats C/C++/ObjC code. [*Added in 0.10*](https://github.com/bitcoin/bitcoin/pull/4498).

./src/addrdb.cpp - Includes code for the classes allowing access to peers.dat (the IP address DB) (CAddrDB) and banlist.dat (the banned node DB) (CBanDB), along with ban list entries (CBanEntry). [*Moved from ./src/net.cpp in 0.14*](https://github.com/bitcoin/bitcoin/pull/8085).

./src/addrdb.h - See the CPP file.

./src/addrman.cpp - [Stochastic address manager](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2012-January/001100.html) (CAddrMan) and CAddress stats (CAddrInfo). In other words, CAddrMan decides what connections to keep in the connection pool, decides what new connections to make, and decides how to respond when a *GetAddr* message comes in. [*Added in 0.6*](https://github.com/bitcoin/bitcoin/pull/787).

./src/addrman.h - See the CPP file.

~~./src/alert.cpp~~ - Alerts for older versions of Core. There’s an unsigned alert with all the data (CUnsignedAlert) and an unsigned alert + signature (CAlert). [*Removed in 0.13*](https://github.com/bitcoin/bitcoin/pull/7692).

~~./src/alert.h~~ - See the CPP file. [*Removed in 0.13*](https://github.com/bitcoin/bitcoin/pull/7692).

~~./src/amount.cpp~~ - Some basic amount (CAmount, or int64\_t) definitions, and a type-safe wrapper class for fee rates (CFeeRate). [*Moved to ./src/policy/feerate.cpp in 0.15*](https://github.com/bitcoin/bitcoin/pull/9279).

./src/amount.h - See the CPP file. Includes a bit of consensus-critical code.

./src/arith\_uint256.cpp - Code for handling unsigned 256-bit big integers (arith\_uint256). *[Added in 0.11](https://github.com/bitcoin/bitcoin/pull/5490)*. Note that this is, in large part, a copy of the original code from ./src/uint256.cpp, which was meant primarily for things like proof-of-work functionality. However, [the arith\_uint256 version is meant only to perform arithmetic functions](https://github.com/bitcoin/bitcoin/pull/5478#issuecomment-67158692); the underlying contents are not to be directly accessed. This is because the arithmetic is required to be compatible with both little and big endian. [Anybody needing direct access to the underlying "blobs" should use the original uint256 class](https://github.com/bitcoin/bitcoin/pull/5490/commits/bfc6070342b9f43bcf125526e6a3c8ed34e29a71), as the arithmetic classes are not to have their underlying memory directly accessed. The arithmetic objects also can't be serialized, unlike the blobs objects.

./src/arith\_uint256.h - See the CPP file. [*Added in 0.11*](https://github.com/bitcoin/bitcoin/pull/5490).

./src/base58.cpp - Base58 implementation.

./src/base58.h - See the CPP file.

./src/bech32.cpp - Code for supporting [BIP 173](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki), aka Base32 address formatting for SegWit outputs, aka "Bech32". [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11167).

./src/bech32.h - See the CPP file. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11167).

~~./src/bignum.h~~ - C++ wrapper around OpenSSL's BIGNUM class (CBigNum). Was used when Core had OpenSSL dependencies in things like the scripting system. [*Moved to ./src/test/bignum.h in 0.11*](https://github.com/bitcoin/bitcoin/pull/4160) because only ./src/test/scriptnum\_tests.cpp still required the CBigNum class.

./src/bitcoin-cli.cpp - Binary used to communicate with / send commands to *bitcoind*.

./src/bitcoin-cli-res.rc - [Resource definition script for Windows.](https://en.wikipedia.org/wiki/Resource_%28Windows%29) Needed for the *bitcoin-cli* binary.

./src/bitcoind.cpp - Command line binary that executes Bitcoin Core functionality. *[Added in 0.9 to accommodate refactoring](https://github.com/bitcoin/bitcoin/pull/2700)*.

./src/bitcoind-res.rc - [Resource definition script for Windows.](https://en.wikipedia.org/wiki/Resource_%28Windows%29) Needed for the *bitcoind* binary.

./src/bitcoin-tx.cpp - Command line binary that can create, parse, or modify transactions.

./src/bitcoin-tx-res.rc - [Resource definition script for Windows.](https://en.wikipedia.org/wiki/Resource_%28Windows%29) Needed for the *bitcoin-tx* binary.

./src/blockencodings.cpp - Implements multiple classes representing objects from [BIP 152](https://github.com/bitcoin/bips/blob/master/bip-0152.mediawiki) (e.g., BlockTransacions, BlockRequest, CBlockHeadAndShortTxIDs), aka Compact Block Relay. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8068).

./src/blockencodings.h - See the CPP file.

./src/blockfilter.cpp - Block filters as defined in [BIP 157](https://github.com/bitcoin/bips/blob/master/bip-0157.mediawiki) and [BIP 158](https://github.com/bitcoin/bips/blob/master/bip-0158.mediawiki). [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12254).

./src/blockfilter.h - See the CPP file. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12254).

./src/bloom.cpp - Bloom filter material. Includes bloom filters (CBloomFilter) and "rolling" filters (CRollingBloomFilter), which tracks the last N items you’ve seen if you can tolerate a small number of false positives. [*Added in 0.8*](https://github.com/bitcoin/bitcoin/pull/1795), with [*rolling filters added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6064).

./src/bloom.h - See the CPP file.

./src/chain.cpp - Covers critical blockchain classes, on-disk and off-disk. There’s the on-disk block position (CDiskBlockPos - *struct*), an entry (final or potential) in the blockchain (CBlockIndex), an on-disk blockchain entry (CDiskBlockIndex), block file info (CBlockFileInfo - [*moved from ./src/main.h in 0.13](https://github.com/bitcoin/bitcoin/pull/7815)) and an in-memory indexed blockchain (CChain). CBlockIndex is [consensus-critical](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2015-September/011161.html). [*Moved out of main.cpp & main.h in 0.10*](https://github.com/bitcoin/bitcoin/pull/4796).

./src/chain.h - See the CPP file.

./src/chainparams.cpp - The parameters for a chain (mainnet, testnet, regtest), including things like the genesis block. CChainParams is the primary class, with a few support structs also defined. [*Added in 0.9*](https://github.com/bitcoin/bitcoin/pull/2632).

./src/chainparams.h - See the CPP file.

./src/chainparamsbase.cpp - A skeletal set of blockchain parameters (e.g., the communications port) for mainnet, testnet, and regtest. Used for network connections. [*Added in 0.10*](https://github.com/bitcoin/bitcoin/pull/4368).

./src/chainparamsbase.h - See the CPP file.

./src/chainparamsseeds.h - Hard-coded "seed" locations. Generated by the devs. [*Added in 0.10*](https://github.com/bitcoin/bitcoin/pull/4582).

./src/checkpoints.cpp - Compiled-in sanity checks. Makes sure a node is on the right chain when getting bootstrapped and also indicates that blocks before a given checkpoint need not be fully verified, as they’re considered too deep in the blockchain to be unwound. [Also prevents a DoS attack.](https://github.com/bitcoin/bitcoin/pull/534)

./src/checkpoints.h - See the CPP file.

./src/checkqueue.h - Queue for scripts to be verified. Parallelization optimization. *[Added in 0.8](https://github.com/bitcoin/bitcoin/pull/2060)*.

./src/clientversion.cpp - Basic build version numbers & string.

./src/clientversion.h - See the CPP file.

./src/coincontrol.h - A class (CCoinControl) specifying a set of coins to be used for a given Tx. (This allows the user to control which coins are used.) [*Added in 0.8*](https://github.com/bitcoin/bitcoin/pull/3253).

./src/coins.cpp - Contains code for a pruned transaction that has only metadata and basically represents UTXOs (CCoins). Also includes various helper structs/classes that do things like abstract the "view" of the UTXO database (CCoinsView) and define the actual UTXO database (CCoinsViewCache), entries in the cache (CCoinsCacheEntry), etc. At a minimum, CCoinsView and CCoinsViewCache are [both](https://github.com/bitcoin/bitcoin/pull/5048#issuecomment-58435406) [consensus-critical](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2015-September/011161.html). [*Moved to the current position in 0.9*](https://github.com/bitcoin/bitcoin/pull/3199).

./src/coins.h - See the CPP file.

./src/compat.h - Code that handles Windows sockets.

./src/compressor.cpp - Compressors for common scripts (CScriptCompressor) and TxOuts (CTxOutCompressor).

./src/compressor.h - See the CPP file.

./src/core\_io.h - [CTransaction hex decode/encode.](https://github.com/bitcoin/bitcoin/pull/4332) Needed by the *bitcoin-tx* binary.

./src/core\_memusage.h - [Core memory computation functions.](https://github.com/bitcoin/bitcoin/pull/6453)

./src/core\_read.cpp - [CTransaction hex decode/encode.](https://github.com/bitcoin/bitcoin/pull/4332) Needed by the *bitcoin-tx* binary.

./src/core\_write.cpp - [CTransaction hex decode/encode.](https://github.com/bitcoin/bitcoin/pull/4332) Needed by the *bitcoin-tx* binary.

./src/cuckoocache.h - A [cuckoo hash table](https://en.wikipedia.org/wiki/Cuckoo_hashing) implementation. Replaces boost::unordered\_set in the CSignatureCache class. Designed to make better utilization of memory, remove the need for locks in some cases, and provide other improvements to the cache functionality. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8895).

./src/dbwrapper.cpp - LevelDB wrapper code. Includes various CDB* classes related to accessing LevelDB.

./src/dbwrapper.h - See the CPP file.

./src/dummywallet.cpp - A dummy wallet used to placate code that doesn't actually use wallets (e.g., *libbitcoin\_server*). [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/14168).

./src/fs.cpp - A filesystem abstraction designed to make it easier to make filesystem changes in one place instead of across many files. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9902).

./src/fs.h - See the CPP file. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9902).

./src/hash.cpp - Hash160 and Hash256 functions, both classes (CHash160/CHash256) and standalone functions.

./src/hash.h - See the CPP file.

./src/httprpc.cpp - Functions that start/stop the HTTP RPC and REST subsystems. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/5677).

./src/httprpc.h - See the CPP file.

./src/httpserver.cpp - Functions related to the HTTP server. Also includes classes for in-flight HTTP requests (HTTPRequest), events (HTTPEvent), and event closure (HTTPClosure). [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/5677)

./src/httpserver.h - See the CPP file.

./src/indirectmap.h - A std::map wrapper that changes the semantics in a subtle manner. Inserts and iterators use pointers since they store pointers and need them to remain constant and dereferenceable, but lookup functions take const references. In other words, an underlying pointer is used as the key, but comparisons are performed using the referenced values. Initially used to make the mempool smaller by removing the CInPoint class (combination of a CTransaction pointer and a uin32\_t index for the appropriate input) and replacing with a const CTransaction pointer. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7997).

./src/init.cpp - Some startup/shutdown functions, help message functions, and license info. Also includes the declaration of the CClientUIInterface object used throughout the CLI and GUI code. (See ./src/ui\_interface.h for more info.) Also includes important notes on thread management and startup/shutdown.

./src/init.h - See the CPP file.

./src/key.cpp - Private keys, encapsulated (CKey class) and serialized (CPrivKey typedef). There’s also a CExtKey and CExtPubKey structs (basically the actual, Base58-encoded private/public keys without the metadata from CBitcoinExtKeyBase) and global ECC start/stop functions.

./src/key.h - See the CPP file.

./src/key\_io.cpp - Bitcoin-specific Base58 functionality (e.g., CBitcoinAddress and CBitcoinSecret classes), along with a derived (from CBase58Data) external class (CBitcoinExtKey) that, when typedef’d, is used for external, Base58-encoded private (CBitcoinExtKeyBase) and public (CBitcoinExtPubKeyBase) keys. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11372).

./src/key\_io.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11372).

./src/keystore.cpp - A key store base class (CKeyStore) and a store with address->secret maps (CBasicKeyStore).

./src/keystore.h - See the CPP file.

./src/limitedmap.h - STL-like map container class that only keeps the N elements with the highest value (limitedmap).

./src/logging.cpp - Basic logging code. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13021).

./src/logging.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13021).

~~./src/main.cpp~~ - Loads of critical functionality. Examples include script op count functions (GetP2SHSigOpCount & the like), checking inputs (CheckInputs), applying Tx effects to the UTXO (UpdateCoins), validity checks (CheckTransaction), consensus-critical functions telling if a Tx is final at a given time/location (IsFinalTx) or in the next block (CheckFinalTx), etc. Also includes the CScriptCheck, and CVerifyDB classes. [*Moved to ./src/net\_processing.{cpp/h} and ./src/validation.{cpp/h} in 0.14*](https://github.com/bitcoin/bitcoin/pull/9260).

./src/main.h - See the CPP file. Includes loads of important definitions.

./src/Makefile.am - Autotool’s Makefile recipe.

./src/Makefile.bench.include - Makefile include file for the *bench\_bitcoin* binary.

./src/Makefile.leveldb.include - Makefile include file for the *LevelDB* library in ./src/leveldb. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8148).

./src/Makefile.qt.include - Makefile include file for the ./src/qt subdirectory.

./src/Makefile.qttest.include - Makefile include file for the ./src/qt/test subdirectory.

./src/Makefile.test.include - Makefile include file for the ./src/test subdirectory.

./src/memusage.h - Some tools to track basic memory usage.

./src/merkleblock.cpp - Tied to Bloom filters. Classes covering partial merkle trees that covers a subset of the TXIDs in a block such that the complete list and the merkle root can be recovered (CPartialMerkleTree), and blocks used to relay headers & vector\<merkle branch\> to filtered nodes (CMerkleBlock). The blocks are what are sent to bloom filters (CBloomFilter).

./src/merkleblock.h - See the CPP file.

./src/miner.cpp - Some critical miner functionality (e.g., CreateNewBlock), and the CBlockTemplate struct.

./src/miner.h - See the CPP file.

./src/net.cpp - Loads of networking functionality. Various classes include but are not limited to signal collectors/message handlers from P2P peers (CNodeSignals struct), node stats (CNodeStats), net messages (CNetMessage), entries in the ban database (banlist.dat) (CBanEntry), node information (CNode), the P2P connection pool manager where we send messages meant for the network (CConnman), and entries in the peer database (peers.dat) (CAddrDB).

./src/net.h - See the CPP file. Includes loads of value definitions and such.

./src/netaddr.cpp - The IP address stuff, including IPv4/IPv6 addresses (CNetAddr), subnets (CSubNet) and IP address + port (CService). [*Moved here from ./src/netbase.cpp in 0.14*](https://github.com/bitcoin/bitcoin/pull/8128).

./src/netaddr.h - See the CPP file.

./src/netbase.cpp - Some basic network items, such as the proxy type (proxyType).

./src/netbase.h - See the CPP file.

./src/netmessagemaker.h - Contains the *CNetMsgMaker* class, which is a shortcut for creating on-the-fly messages suitable for pushing to the *CConnman* class. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9128).

./src/net\_processing.cpp - Contains the network message processing code. [*Added in 0.14 from part of ./src/main.cpp*](https://github.com/bitcoin/bitcoin/pull/9260).

./src/net\_processing.h - See the CPP file. [*Added in 0.14 from part of ./src/main.h*](https://github.com/bitcoin/bitcoin/pull/9260).

./src/noui.cpp - It looks like this is used solely to set up logging signal handlers for *bitcoind* and the test code.

./src/noui.h - See the CPP file.

./src/outputtype.cpp - Code related to the available output transaction types (P2PKH/"legacy," PS2SH-SegWit, and Bech32 as of July 2018). [*Added in 0.17 from part of ./src/wallet/wallet.cpp*](https://github.com/bitcoin/bitcoin/pull/13072).

./src/outputtype.h - See the CPP file. [*Added in 0.17 from part of ./src/wallet/wallet.h*](https://github.com/bitcoin/bitcoin/pull/13072).

./src/pow.cpp - Functions related to difficulty. Consensus-critical.

./src/pow.h - See the CPP file.

./src/prevector.h - vector\<T\> replacement that allocates N elements of T, switching to heap allocation only if more elements are needed. Used only by CScript. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6914).

./src/protocol.cpp - P2P protocol stuff. Includes the message header (CMessageHeader), IP:Port with peer info (CAddress), *Inv* message data (CInv), and NetMsgType and nServices enums.

./src/protocol.h - See the CPP file.

./src/pubkey.cpp - Public key analogue of ./src/key.cpp. Includes a CKey reference (CKeyID), encapsulated public keys (CPubKey), external public keys (CExtPubKey struct), and a handle for the ECC verification module (ECCVerifyHandle).

./src/pubkey.h - See the CPP file.

./src/random.cpp - RNG functions & materials. Uses OpenSSL.

./src/random.h - See the CPP file.

./src/rest.cpp - HTTP REST interface to public blockchain data. [*Added in 0.10*](https://github.com/bitcoin/bitcoin/pull/2844).

./src/reverse\_iterator.h - Template for reverse iteration. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10193).

./src/reverselock.h - [A class replacing boost::reverse\_lock with a local reverse\_lock class.](https://github.com/bitcoin/bitcoin/pull/6630)

./src/scheduler.cpp - Lightweight, simple scheduler for background tasks (CScheduler). [*Added in 0.11*](https://github.com/bitcoin/bitcoin/pull/5964).

./src/scheduler.h - See the CPP file.

./src/serialize.h - General purpose data input/output materials, on-and-off-network, including streaming data. Also includes the VarInt class (CVarInt) and CompactSize functions that can read/write VarInt-compatible values, various #defines, and other miscellaneous functionality.

./src/shutdown.cpp - Shutdown-related functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13235).

./src/shutdown.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13235).

./src/span.h - Adds a "span" data type, similar to Boost's "slice" or C++20's "span". An object that refers to a contiguously laid out set of objects in memory. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12886).

./src/streams.h - Double-ended buffer combining vector and stream-like interfaces (CDataStream), non-refcounted RAII wrapper for FILE*, without (CAutoFile) and with (CBufferedFile) ring buffers that allow the rewinding of X bytes.

./src/sync.cpp - Various synchronization-related mechanisms: Classes, #defs, typedefs, etc.

./src/sync.h - See the CPP file.

./src/threadinterrupt.cpp - Includes CThreadInterrupt, a helper class for interruptible sleeps. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9289).

./src/threadinterrupt.h - See the CPP file. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9289).

./src/threadsafety.h - [Macro annotation code, documenting which locks protect a given piece of data.](https://github.com/bitcoin/bitcoin/pull/2003)

./src/timedata.cpp - Median filter over a stream of values (CMedianFilter). Returns the median of the last N numbers. Also includes functions to keep track of adjusted P2P time.

./src/timedata.h - See the CPP file.

./src/tinyformat.h - [Typesafe drop-in for *sprintf* and logging.](https://github.com/bitcoin/bitcoin/pull/3549)

./src/torcontrol.cpp - Contains functions for enabling and disabling a Tor hidden service. The CPP includes various Tor-related classes used internally. [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/6639)

./src/torcontrol.h - See the CPP file.

./src/txdb.cpp - Tx DB, which is chainstate/ (coin DB) + CCoinsView (CCoinsViewDB). Includes related #defs and such, such as the transaction position in a block file (CDiskTxPos - [*moved from ./src/main.h in 0.13](https://github.com/bitcoin/bitcoin/pull/7815)).

./src/txdb.h - See the CPP file.

./src/txmempool.cpp - Mempool materials. The actual mempool (CTxMemPool), mempool entries (CTxMemPoolEntry), a CCoinsView that apparently reaches into the mempool to get coins (CCoinsViewMemPool), and lots of supports classes and structs.

./src/txmempool.h - See the CPP file. Lots and lots of important comments.

./src/ui\_interface.cpp - Contains basic UI initialization error code. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7787).

./src/ui\_interface.h - Contains CClientUIInterface, the class that handles signals for UI communication.

./src/uint256.cpp - A template class for opaque blobs (base\_blob), derived classes for 160-bit and 256-bit data (uint160 and uint256), and functs for handling 256-bit data strings (uint256S). Originally, this class also performed arithmetic functions. However, [the code was split into "arithmetic" (arith\_uint256) and "opaque" (uint256) classes](https://github.com/bitcoin/bitcoin/pull/5490). This was done [primarily to support big endian CPUs](https://github.com/bitcoin/bitcoin/pull/5510). The opaque version here is basically a blob that relies on the endianness of the system, unlike the arithmetic version (./src/arith\_uint256.cpp), which has arithmetic functionality and doesn't care about endianness but also loses certain functionality (e.g., serialization). Internally, [the blobs are little endian](https://github.com/bitcoin/bitcoin/blob/0.11/src/arith_uint256.cpp#L251) but are [printed as big endian](https://github.com/bitcoin/bitcoin/blob/0.11/src/uint256.cpp#L25). In addition, when creating uint256 values from strings (e.g., incoming RPC calls like *getblock()*), [the endianness of the string is reversed](https://github.com/bitcoin/bitcoin/blob/0.11/src/uint256.cpp#L42-L55).

./src/uint256.h - See the CPP file. Contains the actual uint160 and uint256 classes, along with the base\_blob template class parent.

./src/undo.h - Undo info for CTxIn (CTxInUndo), CTransaction (CTxUndo), and CBlock (CBlockUndo).

./src/util.cpp - Code related to the client/server environment. Used for argument handling, config file parsing, logging (pre-0.17), thread wrappers, global environment setup, Windows network setup, etc.

./src/util.h - See the CPP file.

./src/utilmemory.h - A replacement for [C++14's *make_unique()* function](https://en.cppreference.com/w/cpp/memory/unique_ptr/make_unique). [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13690).

./src/utilmoneystr.cpp - Various money utilities (e.g., *ParseMoney()*).

./src/utilmoneystr.h - See the CPP file.

./src/utilstrencodings.cpp - String utilities (e.g., *DecodeBase32()*).

./src/utilstrencodings.h - See the CPP file.

./src/utiltime.cpp - Time utilities (e.g., *SetMockTime()*).

./src/utiltime.h - See the CPP file.

./src/validation.cpp - Contains block validation code (general, DB, etc.), including the CScriptCheck and CVerifyDB, along with many consensus-critical functs and structs. [*Added in 0.14 from part of ./src/main.cpp*](https://github.com/bitcoin/bitcoin/pull/9260).

./src/validation.h - See the CPP file. [*Added in 0.14 from part of ./src/main.cpp*](https://github.com/bitcoin/bitcoin/pull/9260).

./src/validationinterface.cpp - Has a class (CValidationInterface) that allows modules to hook into startup, shutdown, and node events. Also includes struct (CMainSignals) with signals to listeners. Used to interact with toolslike ØMQ/ZeroMQ.

./src/validationinterface.h - See the CPP file.

./src/version.h - Various version definitions (Core, P2P, etc.).

./src/versionbits.cpp - Implements BIP 9 versionbits logic. [*Added in 0.12.1*](https://github.com/bitcoin/bitcoin/pull/7575).

./src/versionbits.h - See the CPP file. [*Added in 0.12.1*](https://github.com/bitcoin/bitcoin/pull/7575).

./src/versionbitsinfo.cpp - Minimal implementation of a struct with info on features deployed by versionbits usage. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13311).

./src/versionbitsinfo.h - See the CPP file. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13311).

./src/walletinterface.h - Contains wallet interface code, primarily meant to remove wallet dependencies from ./src/init.cpp. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10762).

./src/warnings.cpp - Contains code for dealing with various warnings and warning situations. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9236).

**./src/bench** - Code used to build the *bench\_bitcoin* binary, which does rudimentary code benchmarking. [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/6733)

./src/bench/.gitignore - Files for Git to ignore.

./src/bench/base58.cpp - Base58 encoding/decoding benchmarks. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8107).

./src/bench/bech32.cpp - Bech32 encoding/decoding benchmarks. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13586).

./src/bench/bench.cpp - Code that can be added to other code in order to perform basic benchmarking.

./src/bench/bench.h - See the CPP file.

./src/bench/bench\_bitcoin.cpp - Code that kicks off the *bench\_bitcoin* binary.

./src/bench/block\_assemble.cpp - Benchmarks for block assembly from blocks mined in regtest mode (done to speed up mining). [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13219).

./src/bench/checkblock.cpp - Benchmarks block deserialization and validation (*CheckBlock()*) code. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9049).

./src/bench/checkqueue.cpp - Benchmarks some code related to CCheckQueue. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9498).

./src/bench/crypto\_hash.cpp - Code that benchmarks various crypto hashing algorithms used by Core. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8039).

./src/bench/ccoins\_caching.cpp - Code that benchmarks CCoinsDBView caching. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8873).

./src/bench/coin\_selection.cpp - Code that benchmarks coin selection code. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8873).

~~./src/bench/Examples.cpp~~ - Examples of how to apply the benchmark code. [*Renamed to ./src/bench/examples.cpp in 0.17*](https://github.com/bitcoin/bitcoin/pull/13312).

./src/bench/examples.cpp - Examples of how to apply the benchmark code. [*Renamed from ./src/bench/Examples.cpp in 0.17*](https://github.com/bitcoin/bitcoin/pull/13312).

./src/bench/gfs\_filter.cpp - [Golomb-coded set](http://giovanni.bajo.it/post/47119962313/golomb-coded-sets-smaller-than-bloom-filters) filter benchmarking. (Related to BIP 158.) [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12254).

./src/bench/lockedpool.cpp - Code that benchmarks the LockedPoolManager. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8753).

./src/bench/mempool\_eviction.cpp - Code that benchmarks mempool eviction code. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8873).

./src/bench/merkle\_root.cpp - Code that benchmarks merkle root computation code. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13191).

~~./src/bench/perf.cpp~~ - Code that benchmarks CPU cycles. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9202) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13025)*.

~~./src/bench/perf.h~~ - See the CPP file. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9202) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13025)*.

./src/bench/prevector.cpp - Code that benchmarks various bits of *prevector* (see ./src/prevector.h) functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12549).

~~./src/bench/prevector\_destructor.cpp~~ - Code that benchmarks the destruction of non-trivial prevector objects. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9505) and [*placed inside ./src/bench/prevector.cpp in 0.17*](https://github.com/bitcoin/bitcoin/pull/12549).

./src/bench/rollingbloom.cpp - Code that benchmarks rolling bloom filters. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7934).

./src/bench/verify\_script.cpp - Code that benchmarks script verification code. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8873).

**./src/bench/data** - Data used by code benchmarks. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9049)*.

./src/bench/data/block413567.raw - Contains block 413,567. Used in the *CheckBlock()* benchmarking code. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9049)*.


**./src/compat** - Added to allow Core binaries to be compiled on older computers. *glibc* & *libstdc++*, when compiled into Core on newer machines, will have symbols that are undefined when dynamically linked on older machines. This code can be compiled in to define the newer stuff while allowing dynamic linking for *glibc* & *libstdc++*. *[Added in 0.9.2](https://github.com/bitcoin/bitcoin/pull/4042)*.

./src/compat/byteswap.h - [Endian compatibility.](https://github.com/bitcoin/bitcoin/pull/5510)

./src/compat/endian.h - [Endian compatibility.](https://github.com/bitcoin/bitcoin/pull/5510)

./src/compat/glibc\_compat.cpp - *glibc* compatibility. Used primarily for times when binaries are built with symbols that aren't compatible with older versions of *GCC* and *glibc*. (./contrib/devtools/symbol-check.py is a tool that can expose such holes.) An example is found [here](https://github.com/bitcoin/bitcoin/pull/13171).

./src/compat/glibc\_sanity.cpp - [Tests the environment sanity.](https://github.com/bitcoin/bitcoin/pull/4339)

./src/compat/glibcxx\_sanity.cpp - [Tests the environment sanity.](https://github.com/bitcoin/bitcoin/pull/4339)

./src/compat/sanity.h - [Tests the environment sanity.](https://github.com/bitcoin/bitcoin/pull/4339)

./src/compat/strnlen.cpp - [Provides *strnlen* if not present on the system.](https://github.com/bitcoin/bitcoin/pull/5340)

**./src/config** - ./configure.ac generates ./src/config/bitcoin-config.h dynamically. [AC\_CONFIG\_HEADERS defines the file, and all the output between AC\_INIT and AC\_OUTPUT is placed in the file.](https://www.gnu.org/software/autoconf/manual/autoconf-2.69/html_node/Configuration-Headers.html)

./src/config/.empty - Empty file. [Ensures that Git picks up the directory.](http://stackoverflow.com/a/19399903)

**./src/consensus** - Includes some consensus code *but not all consensus code*, and also not part of *libbitcoinconsensus*.

./src/consensus/consensus.h - Has some important values (e.g., blocksize and sigops).

./src/consensus/merkle.cpp - The merkle tree computation code. [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/6508)

./src/consensus/merkle.h - See the CPP file.

./src/consensus/params.h - Introduces the Consensus namespace, which has some parameters that influence chin consensus.

./src/consensus/tx\_verify.cpp - Transaction validation functions. [*Added in 0.15 from part of ./src/validation.cpp*](https://github.com/bitcoin/bitcoin/pull/8329).

./src/consensus/tx\_verify.h - See the CPP file. [*Added in 0.15 from part of ./src/validation.h*](https://github.com/bitcoin/bitcoin/pull/8329).

./src/consensus/validation.h - Includes a class with info about the block/Tx validation state (CValidationState).

**./src/crypto** - Custom code for standard crypto functs (e.g., SHA-1). [Written primarily to reduce, if not completely remove, Core's reliance on OpenSSL](https://github.com/bitcoin/bitcoin/pull/4100).

./src/crypto/aes.cpp - Wrapper for CTAES library that enables 128/192/256-bit AES encrypt/decrypt, including AES-CBC. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7689).

./src/crypto/aes.h - See the implementation file.

./src/crypto/common.h - Endian-specific in/outs for 16, 32, and 64-bit data. Used for implementations of SHA-256 and RIPEMD-160, along with converting arith\_uint256 values to little endian uint256 values.

./src/crypto/chacha20.cpp - [ChaCha20](https://en.wikipedia.org/wiki/Salsa20#ChaCha_variant) implementation used for PRNG purposes. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9792).

./src/crypto/chacha20.h - See the CPP file. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9792).

./src/crypto/hmac\_sha256.cpp - HMAC-SHA-256 class (CHMAC\_SHA256).

./src/crypto/hmac\_sha256.h - See the CPP file.

./src/crypto/hmac\_sha512.cpp - HMAC-SHA-512 class (CHMAC\_SHA512).

./src/crypto/hmac\_sha512.h - See the CPP file.

./src/crypto/ripemd160.cpp - RIPEMD-160 class (CRIPEMD160).

./src/crypto/ripemd160.h - See the CPP file.

./src/crypto/sha1.cpp - SHA-1 class (CSHA1).

./src/crypto/sha1.h - See the CPP file.

./src/crypto/sha256.cpp - SHA-256 class (CSHA256).

./src/crypto/sha256.h - See the CPP file.

./src/crypto/sha256\_avx2.cpp - [AVX2](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions#AVX2)-optimized SHA-256 code. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13191).

./src/crypto/sha256\_shani.cpp - [Intel SHA Extensions](https://en.wikipedia.org/wiki/Intel_SHA_extensions)-optimized SHA-256 code. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13386).

./src/crypto/sha256\_sse4.cpp - [SSE4](https://en.wikipedia.org/wiki/SSE4)-optimized SHA-256 code. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10821) and [*enabled by default in 0.16*](https://github.com/bitcoin/bitcoin/pull/11176)*.

./src/crypto/sha256\_sse41.cpp - [SSE4.1](https://en.wikipedia.org/wiki/SSE4)-optimized SHA-256 code. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13191).

./src/crypto/sha512.cpp - SHA-512 class (CSHA512).

./src/crypto/sha512.h - See the CPP file.

**./src/crypto/ctaes** - Constant-time AES implementation written by Pieter Wuille. [*Added in 0.13 as a replacement for OpenSSL-dependent functionality*](https://github.com/bitcoin/bitcoin/pull/7689).

./src/crypto/ctaes/bench.c - CTAES benchmarking code. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7689).

./src/crypto/ctaes/COPYING - CTAES license info. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7689).

./src/crypto/ctaes/ctaes.c - Raw constant-time AES implementation. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7689).

./src/crypto/ctaes/ctaes.h - See the implementation file. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7689).

./src/crypto/ctaes/README.md - README explaining the CTAES library, some benchmarks, compilation instructions, and formal code review results. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7689).

./src/crypto/ctaes/test.c - Test suites from FIPS 197 (AES) and SP 800-38A (AES-CBC). [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7689).

**./src/index** - Code related to transaction indexing. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13033).

./src/index/base.cpp - Base class for blockchain data indices. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13243).

./src/index/base.h - See the implementation file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13243).

./src/index/txindex.cpp - Contains the TxClass class, which builds the transaction index concurrently with the main validation thread. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13033).

./src/index/txindex.h - See the implementation file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13033).

**./src/interfaces** - Code used to define boundaries between major components of Core (i.e., node, wallet, and GUI). Not necessarily stable or meant to be used by outside code. *[Added in 0.17](https://github.com/bitcoin/bitcoin/pull/10244) and [renamed in 0.17](https://github.com/bitcoin/bitcoin/pull/12906)*.

./src/interfaces/handler.cpp - Used by the GUi for "handleEvent" methods on interfaces in order to manage their lifetimes. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10244).

./src/interfaces/handler.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10244).

./src/interfaces/node.cpp - Used by the GUI to start and stop Core nodes. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10244).

./src/interfaces/node.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10244).

./src/interfaces/README.md - Explains the defined interfaces. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10244).

./src/interfaces/wallet.cpp - Used by the GUI to access wallets. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10244).

./src/interfaces/wallet.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10244).

**./src/leveldb** - [*LevelDB*](http://leveldb.org/) code maintained by Core. *Will not list individual files (too many)*.

**./src/obj-test** - Doesn’t seem to be used anymore.

./src/obj-test/.gitignore - Files for Git to ignore.

**./src/policy** - Code related to various Core policies (i.e., core functionality in Bitcoin that isn't necessarily consensus-critical). [Added in 0.11](https://github.com/bitcoin/bitcoin/pull/5159).

./src/policy/feerate.cpp - Some basic amount (CAmount, or int64\_t) definitions, and a type-safe wrapper class for fee rates (CFeeRate). [*Moved from ./src/amount.cpp in 0.15*](https://github.com/bitcoin/bitcoin/pull/9279).

./src/policy/feerate.h - See the CPP file. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9279).

./src/policy/fees.cpp - Fee policies and estimation code. Includes various constants, the class estimating the fee/priority required to get coins in a block (CBlockPolicyEstimator), and a class to track historical data on Tx confirmations (TxConfirmStats). [*Added in 0.11*](https://github.com/bitcoin/bitcoin/pull/5159).

./src/policy/fees.h - See the CPP file. Loads of comments explaining the code. [*Added in 0.11*](https://github.com/bitcoin/bitcoin/pull/5159).

./src/policy/policy.cpp - "Standard" functions (*IsStandard()*, *IsStandardTx()*, and *AreInputsStandard()*). [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/6335)

./src/policy/policy.h - Bitcoin policy constants and such. [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/6335)

**./src/primitives** - Some of the most basic building blocks of Bitcoin.

./src/primitives/block.cpp - Block classes (CBlock and CBlockHeader) and a struct showing where in the blockchain that a node, if it doesn’t have a given branch, can find a common trunk.

./src/primitives/block.h - See the CPP file.

./src/primitives/transaction.cpp - Tx classes. Includes a Tx hash and an index *n* into the vout (COutPoint), a Tx input (CTxIn), a Tx output (CTxOut), the Tx placed on the network (CTransaction), and a struct CTransaction that’s mutable (CMutableTransaction).

./src/primitives/transaction.h - See the CPP file.

**./src/qt** - Code related to the GUI version of Bitcoin Core. Code depends on the *Qt* framework.

./src/qt/addressbookpage.cpp - Widget showing a list of send/recv addresses (AddressBookPage).

./src/qt/addressbookpage.h - See the CPP file.

./src/qt/addresstablemodel.cpp - Qt model of the address book that allows views to access and modify the address book (AddressTableModel).

./src/qt/addresstablemodel.h - See the CPP file.

./src/qt/askpassphrasedialog.cpp - Multifunctional dialog to ask for passphrases (AskPassphraseDialog).

./src/qt/askpassphrasedialog.h - See the CPP file.

./src/qt/bantablemodel.cpp - Table showing banned nodes/services. [*Added in 0.12*.](https://github.com/bitcoin/bitcoin/pull/6315)

./src/qt/bantablemodel.h - See the CPP file.

./src/qt/bitcoin\_locale.qrc - [Locale data placed here to allow for deterministic builds.](https://github.com/bitcoin/bitcoin/pull/4323)

./src/qt/bitcoin.cpp - The kickoff code for Bitcoin Core, using the GUI application’s main object (BitcoinApplication).

./src/qt/bitcoin.qrc - Bitcoin app [resource collection file](http://doc.qt.io/qt-5/resources.html).

./src/qt/bitcoinaddressvalidator.cpp - Validator for Base58 (BitcoinAddressEntryValidator) & Bitcoin addresses (BitcoinAddressCheckValidator).

./src/qt/bitcoinaddressvalidator.h - See the CPP file.

./src/qt/bitcoinamountfield.cpp - Widget for entering Bitcoin amounts (BitcoinAmountField).

./src/qt/bitcoinamountfield.h - See the CPP file.

./src/qt/bitcoingui.cpp - The main Bitcoin UI window (BitcoinGUI), communicating with the client & wallet models to give the user an up-to-date core state view.

./src/qt/bitcoingui.h - See the CPP file.

./src/qt/bitcoinstrings.cpp - Strings used by the GUI code.

./src/qt/bitcoinunits.cpp - Bitcoin unit definitions (BitcoinUnits).

./src/qt/bitcoinunits.h - See the CPP file.

./src/qt/callback.h - A workaround solution for Qt 4, where the signals implementation doesn't allow signals to be directly connected to C++11 lambda/closure expressions. A callback QObject with a virtual method that can forward calls to a C++11 lambda/closure is defined. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10098)*.

./src/qt/clientmodel.cpp - Bitcoin network client model (ClientModel).

./src/qt/clientmodel.h - See the CPP file.

./src/qt/coincontroldialog.cpp - [Coin control dialog (CoinControlDialog).](https://github.com/bitcoin/bitcoin/pull/3253)

./src/qt/coincontroldialog.h - See the CPP file.

./src/qt/coincontroltreewidget.cpp - [Coin control tree widget (CoinControlTreeWidget).](https://github.com/bitcoin/bitcoin/pull/3253)

./src/qt/coincontroltreewidget.h - See the CPP file.

./src/qt/csvmodelwriter.cpp - Exports Qt table models to CSV files (CSVModelWriter), making data analysis via a spreadsheet easier.

./src/qt/csvmodelwriter.h - See the CPP file.

./src/qt/editaddressdialog.cpp - Dialog for editing addresses & associated info (EditAddressDialog).

./src/qt/editaddressdialog.h - See the CPP file.

./src/qt/guiconstants.h - Various GUI constants.

./src/qt/guiutil.cpp - Various GUI utility functions (GUIUtil).

./src/qt/guiutil.h - See the CPP file.

./src/qt/intro.cpp - Pre-GUI intro screen (Intro), allowing users to choose data directories & such.

./src/qt/intro.h - See the CPP file.

./src/qt/macdockiconhandler.h - See the MM file.

./src/qt/macdockiconhandler.mm - OS X-specific dock icon handler (MacDockIconHandler).

./src/qt/macnotificationhandler.h - See the MM file.

./src/qt/macnotificationhandler.mm - OS X-specific notification handler (MacNotificationHandler).

./src/qt/Makefile - Kicks off Bitcoin Core (GUI) builds in the parent directory.

./src/qt/modaloverlay.cpp - Implements the *ModalOverlay* class, which enables modal overlays. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8371)*

./src/qt/networkstyle.cpp - [Coin network-specific (e.g., testnet) style info for GUIs (Networkstyle).](https://github.com/bitcoin/bitcoin/pull/4802)

./src/qt/networkstyle.h - See the CPP file.

./src/qt/notificator.cpp - Cross-platform desktop notification client (Notificator).

./src/qt/notificator.h - See the CPP file.

./src/qt/openuridialog.cpp - [Open URI dialog (OpenURIDialog).](https://github.com/bitcoin/bitcoin/pull/3215)

./src/qt/openuridialog.h - See the CPP file.

./src/qt/optionsdialog.cpp - Proxy address widget validator that checks for a valid proxy address (ProxyAddressValidator).

./src/qt/optionsdialog.h - See the CPP file.

./src/qt/optionsmodel.cpp - Interface from Qt to configuration data structure for Bitcoin client (OptionsModel).

./src/qt/optionsmodel.h - See the CPP file.

./src/qt/overviewpage.cpp - Home/Overview page widget (OverviewPage).

./src/qt/overviewpage.h - See the CPP file.

./src/qt/paymentrequest.proto - [Payment request protocol file](https://github.com/bitcoin/bitcoin/pull/2539) [(Google Protocol Buffers).](https://en.wikipedia.org/wiki/Protocol_Buffers)

./src/qt/paymentrequestplus.cpp - [Wraps PaymentRequest (dumb protocol buffer) with PaymentDetails (extra methods) (PaymentRequestPlus).](https://github.com/bitcoin/bitcoin/pull/2539)

./src/qt/paymentrequestplus.h - See the CPP file.

./src/qt/paymentserver.cpp - [Handle payment requests from URI clicks (PaymentServer).](https://github.com/bitcoin/bitcoin/pull/2539)

./src/qt/paymentserver.h - See the CPP file. Lots of important notes.

./src/qt/peertablemodel.cpp - [Qt model providing info about connected peers (PeerTableModel).](https://github.com/bitcoin/bitcoin/pull/4225)

./src/qt/peertablemodel.h - See the CPP file.

./src/qt/platformstyle.cpp - Class (PlatformStyle) that has coin network-specific GUI information. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6487).

./src/qt/platformstyle.h - See the CPP file.

./src/qt/qvalidatedlineedit.cpp - Line edit that can show input validation feedback as "invalid" (QValidatedLineEdit).

./src/qt/qvalidatedlineedit.h - See the CPP file.

./src/qt/qvaluecombobox.cpp - Combo box that can be used to select ordinal values from a model (QValueComboBox).

./src/qt/qvaluecombobox.h - See the CPP file.

./src/qt/README.md - Basic info about the GUI side of Bitcoin Core. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11761).

./src/qt/receivecoinsdialog.cpp - Dialog for receiving Bitcoin payments (ReceiveCoinsDialog).

./src/qt/receivecoinsdialog.h - See the CPP file.

./src/qt/receiverequestdialog.cpp - Dialog for requesting Bitcoin payments (ReceiveRequestDialog) and a label widget for QR codes (QRImageWidget).

./src/qt/receiverequestdialog.h - See the CPP file.

./src/qt/recentrequeststablemodel.cpp - [Model for list of recent payment request/URI generations (RecentRequestsTableModel)](https://github.com/bitcoin/bitcoin/pull/3207), entries (RecentRequestEntry), and entries less than a certain value (RecentRequestEntryLessThan).

./src/qt/recentrequeststablemodel.h - See the CPP file.

./src/qt/rpcconsole.cpp - [Local Bitcoin RPC console (RPCConsole).](https://github.com/bitcoin/bitcoin/pull/1075)

./src/qt/rpcconsole.h - See the CPP file.

./src/qt/sendcoinsdialog.cpp - Dialog for sending Bitcoins (SendCoinsDialog).

./src/qt/sendcoinsdialog.h - See the CPP file.

./src/qt/sendcoinsentry.cpp - Entry in the "Send Bitcoins" dialog (SendCoinsEntry).

./src/qt/sendcoinsentry.h - See the CPP file.

./src/qt/signverifymessagedialog.cpp - [Message sign/verification window (SignVerifyMessageDialog).](https://github.com/bitcoin/bitcoin/pull/1469)

./src/qt/signverifymessagedialog.h - See the CPP file.

./src/qt/splashscreen.cpp - GUI splash screen w/ version info (SplashScreen).

./src/qt/splashscreen.h - See the CPP file.

./src/qt/trafficgraphwidget.cpp - [Network traffic graph (TrafficGraphWidget).](https://github.com/bitcoin/bitcoin/pull/2924)

./src/qt/trafficgraphwidget.h - See the CPP file.

./src/qt/transactiondesc.cpp - Human-readable HTML description of a Tx (TransactionDesc).

./src/qt/transactiondesc.h - See the CPP file.

./src/qt/transactiondescdialog.cpp - Dialog showing Tx details (TransactionDescDialog).

./src/qt/transactiondescdialog.h - See the CPP file.

./src/qt/transactionfilterproxy.cpp - Filter Tx list according to rules (TransactionFilterProxy).

./src/qt/transactionfilterproxy.h - See the CPP file.

./src/qt/transactionrecord.cpp - UI model for Tx status (TransactionStatus).

./src/qt/transactionrecord.h - See the CPP file.

./src/qt/transactiontablemodel.cpp - UI model for a wallet’s Tx table (TransactionTableModel).

./src/qt/transactiontablemodel.h - See the CPP file.

./src/qt/transactionview.cpp - Widget showing a wallet’s Tx list (TransactionView).

./src/qt/transactionview.h - See the CPP file.

./src/qt/utilitydialog.cpp - ["Help message" (HelpMessageDialog) and "Shutdown" (ShutdownWindow) dialog boxes.](https://github.com/bitcoin/bitcoin/pull/3548)

./src/qt/utilitydialog.h - See the CPP file.

./src/qt/walletframe.cpp - [Embeds all wallet-related controls (WalletFrame).](https://github.com/bitcoin/bitcoin/pull/2220)

./src/qt/walletframe.h - See the CPP file.

./src/qt/walletmodel.cpp - [Interface to Bitcoin wallet from Qt view (WalletModel)](https://github.com/bitcoin/bitcoin/pull/521) and coin recipients (SendCoinsRecipient).

./src/qt/walletmodel.h - See the CPP file.

./src/qt/walletmodeltransaction.cpp - [Data model for wallet model Txs (WalletModelTransaction).](https://github.com/bitcoin/bitcoin/pull/2958)

./src/qt/walletmodeltransaction.h - See the CPP file.

./src/qt/walletview.cpp - [Handles wallet page view renderings & updates (WalletView).](https://github.com/bitcoin/bitcoin/pull/2220)

./src/qt/walletview.h - See the CPP file.

./src/qt/winshutdownmonitor.cpp - [Catch Windows shutdown events (WinShutdownMonitor).](https://github.com/bitcoin/bitcoin/pull/4043)

./src/qt/winshutdownmonitor.h - See the CPP file.

**./src/qt/forms** - [*Q*t](http://doc.qt.io/qt-5.5/designer-using-a-ui-file.html)[ Designer files](http://doc.qt.io/qt-5.5/designer-using-a-ui-file.html) (XML) used to generate .h/.cpp files for graphics layouts.

./src/qt/forms/addressbookpage.ui - Address book dialog layout.

./src/qt/forms/askpassphrasedialog.ui - Wallet passphrase dialog layout.

./src/qt/forms/coincontroldialog.ui - [Coin control address selection dialog layout.](https://github.com/bitcoin/bitcoin/pull/3253)

./src/qt/forms/debugwindow.ui - [RPC console/debug window layout.](https://github.com/bitcoin/bitcoin/pull/1075)

./src/qt/forms/editaddressdialog.ui - Bitcoin address edit dialog layout.

./src/qt/forms/helpmessagedialog.ui - [Help message dialog layout.](https://github.com/bitcoin/bitcoin/pull/3548)

./src/qt/forms/intro.ui - [Data directory selection dialog layout.](https://github.com/bitcoin/bitcoin/pull/2670)

./src/qt/forms/openuridialog.ui - ["Open URI" dialog layout.](https://github.com/bitcoin/bitcoin/pull/3215)

./src/qt/forms/optionsdialog.ui - [Options dialog layout.](https://github.com/bitcoin/bitcoin/pull/1433)

./src/qt/forms/overviewpage.ui - [Home/Overview dialog layout.](https://github.com/bitcoin/bitcoin/pull/1433)

./src/qt/forms/receivecoinsdialog.ui - ["Receive coins" dialog layout.](https://github.com/bitcoin/bitcoin/pull/3099)

./src/qt/forms/receiverequestdialog.ui - ["Request coins" dialog layout.](https://github.com/bitcoin/bitcoin/pull/3099)

./src/qt/forms/sendcoinsdialog.ui - "Send coins" dialog layout.

./src/qt/forms/sendcoinsentry.ui - "Send coins" entry dialog layout.

./src/qt/forms/signverifymessagedialog.ui - ["Sign/Verify message" dialog layout.](https://github.com/bitcoin/bitcoin/pull/1469)

./src/qt/forms/transactiondescdialog.ui - Tx description dialog layout.

**./src/qt/locale** - Core translations. *Files not listed.*

**./src/qt/res** - Qt resources.

./src/qt/res/bitcoin-qt-res.rc - Windows resource file for the Bitcoin Core GUI.

**./src/qt/res/icons** - PNG graphics files for Core. *Files not listed.* 

**./src/qt/res/movies** - PNG movie/animation files for Core. *Files not listed.*

**./src/qt/res/src** - SVG icon "source" files for Core. *Files not listed.*

**./src/qt/test** - Bitcoin Core (GUI) test code.

./src/qt/test/addressbooktests.cpp - Address book manipulation tests. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12830).

./src/qt/test/addressbooktests.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12830).

./src/qt/test/compattests.cpp - Some Qt cross-platform compatibility tests. It started with *bswap\_{16/32/64}()* calls to ensure that the macOS build functions properly, particularly with protobuf defining its own bswap calls. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9366).

./src/qt/test/compattests.h - See the CPP file. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9366).

./src/qt/test/Makefile - Makefile kicking off Bitcoin Core (GUI) test build code in the parent directory.

./src/qt/test/paymentrequestdata.h - [Data for ./src/qt/tests/paymentservertests.cpp.](https://github.com/bitcoin/bitcoin/pull/2539)

./src/qt/test/paymentservertests.cpp - [Payment Protocol (BIP 70) test code.](https://github.com/bitcoin/bitcoin/pull/2539)

./src/qt/test/paymentservertests.h - See the CPP file.

./src/qt/test/rpcnestedtests.cpp - Tests the ability of the RPC console to support nested commands and simple value queries. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/7783).

./src/qt/test/rpcnestedtests.h - See the CPP file.

./src/qt/test/test\_main.cpp - [Bitcoin Core (GUI) test suite kickoff file.](https://github.com/bitcoin/bitcoin/pull/807)

./src/qt/test/uritests.cpp - [Bitcoin URI test code.](https://github.com/bitcoin/bitcoin/pull/987)

./src/qt/test/uritests.h - See the CPP file.

./src/qt/test/util.cpp - Qt test utilities (e.g., pressing a button). [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12830).

./src/qt/test/util.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12830).

./src/qt/test/wallettests.cpp - Basic wallet tests (e.g., sending coins). [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9974).

./src/qt/test/wallettests.h - See the CPP file.

**./src/rpc** - General RPC functionality. *[Most files moved from ./src to ./src/rpc in 0.13](https://github.com/bitcoin/bitcoin/pull/7348).*

./src/rpc/blockchain.cpp - RPC blockchain command functionality.

./src/rpc/blockchain.h - See the CPP file. As of the initial commit, the only functionality is the prototype for a function getting the difficulty given a block index (or the chain tip if not provided). [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10095).

./src/rpc/client.cpp - RPC client functionality.

./src/rpc/client.h - See the CPP file.

./src/rpc/mining.cpp - RPC mining command functionality, including *getblocktemplate()*.

./src/rpc/mining.h - See the CPP file. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10683).

./src/rpc/misc.cpp - RPC miscellaneous command functionality.

./src/rpc/net.cpp - RPC network command functionality.

./src/rpc/protocol.cpp - RPC protocol commands/enums/etc.

./src/rpc/protocol.h - See the CPP file.

./src/rpc/rawtransaction.cpp - RPC raw transaction command functionality.

./src/rpc/rawtransaction.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10579).

./src/rpc/register.h - Contains prototypes for functions used to register various types of RPC commands. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7766).

~~./src/rpc/safemode.cpp~~ - Has an "ObserveSafeMode" function that checks whether or not "safe mode" (a now-disabled feature the [disabled some RPC commands](https://github.com/bitcoin/bitcoin/pull/10563)) has been activated. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11179) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13090)*.

~~./src/rpc/safemode.h~~ - See the CPP file. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11179) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/13090)*.

./src/rpc/server.cpp - RPC server functionality.

./src/rpc/server.h - See the CPP file.

./src/rpc/util.cpp - Miscellaneous utilities (e.g., retrieve a given pub key for a given address). [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11415).

./src/rpc/util.h - See the CPP file. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11415).

**./src/script** - Code that handles Bitcoin scripts. *[Moved to the current location in 0.10 to make the code more modular](https://github.com/bitcoin/bitcoin/pull/4754)*.

./src/script/bitcoinconsensus.cpp - Some consensus-critical code, centered primarily around script verification.

./src/script/bitcoinconsensus.h - See the CPP file.

./src/script/descriptor.cpp - Code that outputs human-readable descriptions of scriptPubKey objects. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13697).

./src/script/descriptor.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13697).

./src/script/interpreter.cpp - Covers transaction signature checking. BaseSignatureChecker class, which is the parent of TransactionSignatureChecker and MutableTransactionSignatureChecker. Loads of code and comments. [Consensus-critical](https://github.com/bitcoin/bitcoin/pull/12885).

./src/script/interpreter.h - See the CPP file. Also includes many script hash & verification flags.

./src/script/ismine.cpp - Helps determine the wallet type and how many keys are in the wallet. [*Moved here from ./src/wallet in 0.13*](https://github.com/bitcoin/bitcoin/pull/7905).

./src/script/ismine.h - See the CPP file. [*Moved here from ./src/wallet in 0.13*](https://github.com/bitcoin/bitcoin/pull/7905).

./src/script/script.cpp - Covers classes like the serialized script used in Tx inputs & outputs (CScript), and the class that enforces the arithmetic operation semantics of opcodes (CScriptNum). [Consensus-critical](https://github.com/bitcoin/bitcoin/pull/12885).

./src/script/script.h - See the CPP file. Has the script enums and related script constants.

./src/script/script\_error.cpp - Defines script errors.

./src/script/script\_error.h - See the CPP file.

./src/script/sigcache.cpp - Caches signatures so that a Tx’s signature doesn’t have to be verified twice (entry into the mempool and into the blockchain). Includes a child of TransactionSignatureChecker (CachingTransactionSignatureChecker). The CPP file has several helper classes not in the header.

./src/script/sigcache.h - See the CPP file.

./src/script/sign.cpp - Signature creation. Includes the virtual base (BaseSignatureCreator), creator for transactions (TransactionSignatureCreator), creator of empty 72 byte signatures (DummySignatureCreator), and various helper functions.

./src/script/sign.h - See the CPP file.

./src/script/standard.cpp - Code related to standard transaction types (e.g., P2PKH, P2SH, etc.). Some functions and a Hash160 of the script’s serialization (CScriptID).

./src/script/standard.h - See the CPP file.

**./src/secp256k1** - Downstream version of the libsecp256k1 library. This is the library that performs all cryptographic functions related to creating and verifying signatures for Bitcoin transactions. *No files listed. Consult the libsecp256k1 doc or the [project website](https://github.com/bitcoin-core/secp256k1)*.

**./src/support** - Used primarily to abstract out some low-level functionality supplied by OpenSSL, Boost, and libevent. Makes code changes a lot easier since changes occur only in one place.

./src/support/cleanse.cpp - [Abstracts a memory "cleanse" provided by OpenSSL.](https://github.com/bitcoin/bitcoin/pull/5689)

./src/support/cleanse.h - See the CPP file.

./src/support/events.h - Applies [RAII](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization) principles to *libevent*. Various *libevent* types are wrapped with unique\_ptr\<\> and given deleters to make pointer handling and such, for the most part, automated inside the Core code. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9387).

./src/support/lockedpool.cpp - Intended as a LockedPageManager replacement (from ./src/support/pagelocker.cpp). Includes LockedPoolManager, a singleton class tracking locked (non-swappable) memory for use in std::allocator templates. There are several support classes: An OS-dependent (de)allocator of locked/pinned memory pages (LockedPageAllocator), a manager of contiguous memory (Arena), and a pool for locked memory chunks (LockedPool). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8753).

./src/support/lockedpool.h - See the CPP file. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8753).

~~./src/support/pagelocker.cpp~~ - [Deals with memory locking.](https://github.com/bitcoin/bitcoin/pull/5952) Includes an OS-dependent memory lock/unlock class (MemoryPageLocker), a thread-safe base class that keeps track of locked (i.e., non-swappable) memory pages (LockedPageManagerBase), and a derived singleton class that tracks locked memory pages for use in std::allocator templates (LockedPageManager). [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8753).

~~./src/support/pagelocker.h~~ - See the CPP file. [*Removed in 0.14*](https://github.com/bitcoin/bitcoin/pull/8753).

**./src/support/allocators** - Secure memory allocation/deallocation code.

./src/support/allocators/secure.h - Secure memory allocation (secure\_allocator struct).

./src/support/allocators/zeroafterfree.h - Safe memory deallocation (zero\_after\_free\_allocator struct).

**./src/test** - [Unit tests for internal (i.e., not outward-facing, like RPC calls) source code.](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2014-July/006379.html) Uses Boost’s test framework. Can be built with *make check* and run with the *test\_bitcoin* binary.

./src/test/addrman\_tests.cpp - Tests for the CAddrMan class. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6720).

~~./src/test/alert\_tests.cpp~~ - [Alert system (CAlert) unit tests.](https://github.com/bitcoin/bitcoin/pull/1393) Used to determine if a set of blocks are getting fed to the system too quickly or slowly. [*Removed in 0.13*](https://github.com/bitcoin/bitcoin/pull/8275).

./src/test/allocator\_tests.cpp - Memory allocation tests. [Has to do with memory "stacking."](https://github.com/bitcoin/bitcoin/pull/1699)

./src/test/amount\_tests.cpp - Tests the fee rates. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7705).

./src/test/arith\_uint256\_tests.cpp - uint256 ("opaque") and arith\_uint256 ("arithmetic") testing. *[Added in 0.11](https://github.com/bitcoin/bitcoin/pull/5490)*.

./src/test/base32\_tests.cpp - Base32 unit tests.

./src/test/base58\_tests.cpp - Base58 unit tests.

./src/test/base64\_tests.cpp - Base64 unit tests.

./src/test/bech32\_tests.cpp - Bech32 unit tests. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11167).

~~./src/test/bctest.py~~ - [Support code for *bitcoin-tx* binary test](https://github.com/bitcoin/bitcoin/pull/4624). [*Moved to ./test/util/bctest.py in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

~~./src/test/bignum.h~~ - See the ./src/bignum.h entry. [*Removed in 0.12*](https://github.com/bitcoin/bitcoin/pull/7095) and replaced with ./src/test/scriptnum10.h.

~~./src/test/bitcoin-util-test.py~~ - [Kicks off *bitcoin-tx* binary test](https://github.com/bitcoin/bitcoin/pull/4624). [*Moved to ./test/util/bitcoin-util-test.py in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

./src/test/bip32\_tests.cpp - [Hierarchical deterministic (HD) wallet unit tests.](https://github.com/bitcoin/bitcoin/pull/2829)

~~./src/test/bitcoin-util-test.py~~ - [Kicks off *bitcoin-tx* binary test](https://github.com/bitcoin/bitcoin/pull/4624). [*Moved to ./test/util/bitcoin-util-test.py in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

./src/test/blockchain\_tests.cpp - Implements GetDifficulty tests and other blockchain-related tests. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11748).

./src/test/blockencodings\_test.cpp - Implements Compact Block Relay tests. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/8068).

./src/test/blockfilter\_tests.cpp - Tests related to BIP 157-associated block filters. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12254).

./src/test/bloom\_tests.cpp - [CBloomFilter and CMerkleBlock unit tests.](https://github.com/bitcoin/bitcoin/pull/1795)

./src/test/bswap\_tests.cpp - Tests *bswap\_{16/32/64}()* calls to ensure that the calls function properly. (This was a problem in particular on macOS builds.) [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9366).

~~./src/test/buildenv.py.in~~ - [Helps allow Python tests to run on Windows](https://github.com/bitcoin/bitcoin/pull/5014). [*Moved to ./test/util/buildenv.py.in in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

~~./src/test/checkblock\_tests.cpp~~ - Now-obsolete test that [was used](https://github.com/bitcoin/bitcoin/commit/8c222dca4f961ad13ec64d690134a40d09b20813) to confirm that Core would handle 1 MB blocks after the temporary 500 KB soft fork imposed in the wake of the Mar. 2013 hard fork. [*Removed in 0.13*](https://github.com/bitcoin/bitcoin/pull/7490).

~~./src/test/Checkpoints\_tests.cpp~~ - A checkpoint-related unit test. *[Removed in 0.13.2](https://github.com/bitcoin/bitcoin/pull/9293)*. This was [part of a larger push to remove checkpoints and replace them with most-work chain metrics](https://github.com/bitcoin/bitcoin/pull/9053).

./src/test/checkqueue\_tests.cpp - Various CCheckQueue tests. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9497).

./src/test/coins\_tests.cpp - [Tests for CCoinsView and related classes.](https://github.com/bitcoin/bitcoin/pull/4834)

./src/test/compress\_tests.cpp - [Tests for amount serializer/deserializer code.](https://github.com/bitcoin/bitcoin/pull/1677)

./src/test/crypto\_tests.cpp - SHA (regular and HMAC) and RIPEMD-160 unit tests.

./src/test/cuckoocache\_tests.cpp - Provides some unit tests for the cuckoo hash table implementation in ./src/cuckoocache.h. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8895).

./src/test/dbwrapper\_tests.cpp - Tests for the LevelDB wrappers.

./src/test/denialofservice\_tests.cpp - Denial of Service unit tests. [*Renamed from ./src/test/DoS\_tests.cpp in 0.17*](https://github.com/bitcoin/bitcoin/pull/13312).

./src/test/descriptor\_tests.cpp - Unit tests for human-readable scriptPubKey descriptors. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13697).

~~./src/test/DoS\_tests.cpp~~ - Denial of Service unit tests. [*Renamed to ./src/test/denialofservice\_tests.cpp in 0.17*](https://github.com/bitcoin/bitcoin/pull/13312).

./src/test/getarg\_tests.cpp - *GetArg()* and *GetBoolArg()* unit tests.

./src/test/hash\_tests.cpp - *MurmurHash3()* unit tests. [Useful for Bloom filter work.](https://github.com/bitcoin/bitcoin/pull/2915)

./src/test/key\_properties.cpp - Unit tests (property-based) for key generation, using *rapidcheck*. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12775).

./src/test/key\_tests.cpp - [EC key unit tests.](https://github.com/bitcoin/bitcoin/pull/649)

./src/test/key\_io\_tests.cpp - Bitcoin-specific Base58 functionality tests. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11372).

./src/test/limitedmap\_tests.cpp - Tests for the *limitedmap* class.

./src/test/main\_tests.cpp - [Unit tests related to money supplies.](https://github.com/bitcoin/bitcoin/pull/3768)

./src/test/Makefile - Used to kick off the *bitcoin\_test* binary build elsewhere.

./src/test/mempool\_tests.cpp - Mempool unit tests.

./src/test/merkleblock\_tests.cpp - Tests the merkle block (CMerkleBlock) code. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11293)*.

./src/test/miner\_tests.cpp - Various miner-related unit tests.

./src/test/multisig\_tests.cpp - Various multisig-related unit tests.

./src/test/net\_tests.cpp - Used to test CAddrDB and ensure that CAddrMan objects aren't corrupted. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7696).

./src/test/netbase\_tests.cpp - Some unit tests for basic network functionality (netbase).

./src/test/pmt\_tests.cpp - [CPartialMerkleTree (Bloom filter) unit tests.](https://github.com/bitcoin/bitcoin/pull/1795)

./src/test/policyestimator\_tests.cpp - Policy fee estimation unit tests. [*Added in 0.11*](https://github.com/bitcoin/bitcoin/pull/5159).

./src/test/pow\_tests.cpp - [Unit tests for next difficulty calculations.](https://github.com/bitcoin/bitcoin/pull/5813)

./src/test/prevector\_tests.cpp - Tests for the *prevector* class.

./src/test/raii\_event\_tests.cpp - Tests for RAII-styled handling of *libevent* objects. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9387).

./src/test/random\_tests.cpp - Tests OS-specific random number generation calls for Linux and various BSD OSes (i.e., not /dev/urandom). [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9821).

./src/test/README.md - Explains how to run the unit tests.

./src/test/reverselock\_tests.cpp - Tests for the *reverse\_lock* class.

./src/test/rpc\_tests.cpp - Internal RPC/JSON unit tests.

./src/test/sanity\_tests.cpp - [Compiler sanity check unit tests.](https://github.com/bitcoin/bitcoin/pull/5604)

./src/test/script\_standard\_tests.cpp - Testing for standard script functionality (success and failure). [*Added in 0.15.1*](https://github.com/bitcoin/bitcoin/pull/11116).

./src/test/scriptnum10.h - Class implementing the CScriptNum implementation from Core 0.10.0 (CScriptNum10), which itself was a replacement for the CBigNum class (i.e., a class with an OpenSSL dependency). [Used for comparison purposes and the removal of another OpenSSL dependency in the test code](https://github.com/bitcoin/bitcoin/pull/7086). [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/7095).

./src/test/scheduler\_tests.cpp - [CScheduler unit tests.](https://github.com/bitcoin/bitcoin/pull/5964)

~~./src/test/script\_P2SH\_tests.cpp~~ - Unit tests for the inner workings of P2SH scripts. [*Renamed to ./src/test/script\_p2sh\_tests.cpp in 0.17*](https://github.com/bitcoin/bitcoin/pull/13312).

./src/test/script\_p2sh\_tests.cpp - Unit tests for the inner workings of P2SH scripts. [*Renamed from ./src/test/script\_P2SH\_tests.cpp in 0.17*](https://github.com/bitcoin/bitcoin/pull/13312).

./src/test/script\_tests.cpp - Unit tests for general script validity.

./src/test/scriptnum\_tests.cpp - CScriptNum unit tests. Added to ensure that CScriptNum continued to function properly after the scripting system removed its OpenSSL dependency. [*Added in 0.10*](https://github.com/bitcoin/bitcoin/pull/3965).

./src/test/serialize\_tests.cpp - [CVarInt unit tests](https://github.com/bitcoin/bitcoin/pull/1677).

./src/test/sighash\_tests.cpp - [Sighash flag unit tests](https://github.com/bitcoin/bitcoin/pull/2645).

./src/test/sigopcount\_tests.cpp - [Sigop count unit tests](https://github.com/bitcoin/bitcoin/pull/748).

./src/test/skiplist\_tests.cpp - [Skip list (related to CBlockIndex/headers-first block propagation) unit tests](https://github.com/bitcoin/bitcoin/pull/4420).

./src/test/streams\_tests.cpp - Tests the *CDataStream* class. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6650).

./src/test/sync\_tests.cpp - Tests for lock (threading) functionality. [*Added in 0.18*.](https://github.com/bitcoin/bitcoin/pull/11640).

./src/test/test\_bitcoin.cpp - Some basic test setup code and other functionality (e.g., testing insecure random number generation). Mainly used to configure logging and chain parameters.

./src/test/test\_bitcoin.h - See the CPP file.

./src/test/test\_bitcoin\_fuzzy.cpp - A basic fuzzing harness meant to be used with [American Fuzzy Lop (AFL)](http://lcamtuf.coredump.cx/afl/) or [libFuzzer](https://llvm.org/docs/LibFuzzer.html). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/9172).

./src/test/test\_bitcoin\_main.cpp - Contains the Boost.Test main function and some global overrides. [Makes ./src/test/test\_bitcoin.cpp compatible with the Qt test framework](https://github.com/bitcoin/bitcoin/pull/9974/commits/91e303595be2cc2361a5e32000e23a3b744e2fc1). [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9974).

./src/test/test\_random.h - Adds some tests for the FastRandomContext class, which takes secure random input and then quickly outputs insecure, deterministic data (mainly useful for tests, where secure random data usually isn't needed). *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8914) and [deleted and moved to ./src/test/test\_bitcoin.h in 0.15](https://github.com/bitcoin/bitcoin/pull/10321)*.

./src/test/testutil.cpp - Returns temporary file paths. To be used in tests only due to unchecked error conditions. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7667) and [removed in 0.15.1](https://github.com/bitcoin/bitcoin/pull/11234)*.

./src/test/testutil.h - See the CPP file. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7667) and [removed in 0.15.1](https://github.com/bitcoin/bitcoin/pull/11234)*.

./src/test/timedata\_tests.cpp - [CMedianFilter unit tests.](https://github.com/bitcoin/bitcoin/pull/4748)

./src/test/torcontrol\_tests.cpp - Unit tests for Tor reply parsers. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10408).

./src/test/transaction\_tests.cpp - Transaction unit tests.

./src/test/txindex\_tests.cpp - Unit test for the *TxIndex* class. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13033).

./src/test/txvalidation\_tests.cpp - Tests the mempool rejecting coinbase transactions. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11714).

./src/test/txvalidationcache\_tests.cpp - [Test ensuring that a block with a double spend in it doesn't pass validation if half of the double spend is already in the memory pool (so full-blown transaction validation is skipped) when the block is received.](https://github.com/bitcoin/bitcoin/pull/6077)

./src/test/uint256\_tests.cpp - Unit tests for uint256, arith\_uint256 and related classes.

~~./src/test/univalue\_tests.cpp~~ - [Unit tests for the UniValue class.](https://github.com/bitcoin/bitcoin/pull/4730) *[Removed in 0.16](https://github.com/bitcoin/bitcoin/pull/11879) once the UniValue code [added the test](https://github.com/bitcoin-core/univalue/pull/4) and the new version was [added to Core](https://github.com/bitcoin/bitcoin/pull/11420)*.

./src/test/util\_tests.cpp - Unit tests for various utility-related files.

./src/test/validation\_block\_tests.cpp - Unit tests for signals generated by the *ProcessNewBlock* function. [*Added in 0.16.1*](https://github.com/bitcoin/bitcoin/pull/13023).

./src/test/versionbits\_tests.cpp - Tests the BIP 9 deployment logic. [*Added in 0.12.1*](https://github.com/bitcoin/bitcoin/pull/7543).

**./src/test/data** - Data for unit tests. [Data is built into the binary](https://github.com/bitcoin/bitcoin/pull/2985) via ./src/Makefile.test.include, which takes the .json files in this ./src/test/data subdirectory and creates .json.h files. The .h files are then compiled into the *./src/test/test\_bitcoin* binary. [*Many files moved to ./test/util/data in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

./src/test/data/base58\_encode\_decode.json - Base58 test data used by ./src/tests/base58\_tests.cpp to confirm that encoding & decoding work. [Generated by ./contrib/testgen/gen\_base58\_test\_vectors.py](https://github.com/bitcoin/bitcoin/pull/1888).

./src/test/data/base58\_keys\_invalid.json - Base58 test data used by ./src/tests/base58\_tests.cpp to confirm that the given Base58 keys are invalid across various key types. [Generated by ./contrib/testgen/gen\_base58\_test\_vectors.py](https://github.com/bitcoin/bitcoin/pull/1888).

./src/test/data/base58\_keys\_valid.json - Base58 test data used by ./src/tests/base58\_tests.cpp to confirm that the given Base58 keys are valid across various key types. [Generated by ./contrib/testgen/gen\_base58\_test\_vectors.py.](https://github.com/bitcoin/bitcoin/pull/1888)

./src/test/data/blockfilters.json - Data for tests related to BIP 157-associated block filters. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12254).

./src/test/data/key\_io\_invalid.json - Base58 test data used by ./src/tests/key\_io\_tests.cpp to confirm that the given Base58 keys are invalid across various key types. [*Moved from ./src/test/data/base58\_keys\_invalid.json in 0.17*](https://github.com/bitcoin/bitcoin/pull/11372).

./src/test/data/key\_io\_valid.json - Base58 test data used by ./src/tests/key\_io\_tests.cpp to confirm that the given Base58 keys are valid across various key types. [*Moved from ./src/test/data/base58\_keys\_valid.json in 0.17*](https://github.com/bitcoin/bitcoin/pull/11372).

./src/test/data/README.md - Mentions that this is data for various tests.

./src/test/data/script\_tests.json - Data for valid and invalid scripts. [Used by ./src/tests/script\_tests.cpp](https://github.com/bitcoin/bitcoin/pull/1121).

./src/test/data/sighash.json - Sighash data. [Used by ./src/tests/sighash\_tests.cpp](https://github.com/bitcoin/bitcoin/pull/3975).

./src/test/data/tx\_invalid.json - *bitcoin-tx -delin=1* test data. Consists of invalid, deserialized transactions. [Used by ./src/test/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4733)

./src/test/data/tx\_valid.json - *bitcoin-tx -delin=1* test data. Consists of valid, deserialized transactions, [including one Tx that was valid pre-BIP66](https://github.com/bitcoin/bitcoin/pull/11077). [Used by ./src/test/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4733)

**./src/test/gen** - Data generated for property-based test sets. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/12775).

./src/test/gen/crypto\_gen.cpp - Data generated for key-based property tests using *rapidcheck*. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12775).

./src/test/gen/crypto\_gen.h - See the CPP file. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/12775).

**./src/univalue** - Downstream version of the libunivalue library. Objects are used for parsing and encoding JSON data. [Replaced JSON Spirit.](https://github.com/bitcoin/bitcoin/pull/6121) *No files listed. [Consult the project website](https://github.com/jgarzik/univalue)*.

**./src/wallet** - Core’s wallet functionality. Any code here should be used solely by the wallet.

./src/wallet/coincontrol.cpp -  A class (CCoinControl) specifying a set of coins to be used for a given Tx. (This allows the user to control which coins are used.) [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12257).

./src/wallet/coincontrol.h -See the CPP file. *[Added to the src subdirectory in 0.8](https://github.com/bitcoin/bitcoin/pull/3253), and [moved to the src/wallet subdirectory in 0.14](https://github.com/bitcoin/bitcoin/pull/8990)*.

./src/wallet/coinselection.cpp - Code for selecting coins based on the ["Branch and Bound" algorithm](http://murch.one/wp-content/uploads/2016/11/erhardt2016coinselection.pdf), falling back to Core's previous coin selection algorithm if the algorithm fails. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10637).

./src/wallet/coinselection.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10637).

./src/wallet/crypter.cpp - Includes the master key class for a wallet’s private key encryption (CMasterKey), encryption/decryption context class w/ key info (CCrypter), and a keystore keeping the private keys (CCryptoKeyStore).

./src/wallet/crypter.h - See the CPP file.

./src/wallet/db.cpp - Classes providing access to a BerkeleyDB instance (CDB) and the DB’s environment (CDBEnv).

./src/wallet/db.h - See the CPP file.

./src/wallet/feebumper.cpp - Contains code related to wallet fee bumping (CFeeBumper and helper functions). [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9681).

./src/wallet/fees.cpp - Static fee-related code, taken from ./src/wallet/wallet.cpp. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/10976).

./src/wallet/fees.h - See the CPP file. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/10976).

./src/wallet/feebumper.h - See the CPP file. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9681).

./src/wallet/init.cpp - Static wallet initialization code, taken from ./src/wallet/wallet.cpp. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/10976).

~~./src/wallet/init.h~~ - See the CPP file. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/10976) and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/12836)*.

./src/wallet/rpcdump.cpp - RPC functions related to exporting/importing wallet info, addresses, etc.

./src/wallet/rpcwallet.cpp - RPC functionality not related to exporting/importing wallet info & such.

./src/wallet/rpcwallet.h - See the CPP file. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7307)*.

./src/wallet/wallet.cpp - The basic wallet functionality. Includes many constants & policy defaults, keypool entries (CKeyPool), address book data (CAddressBookData), Tx w/ merkle branch linking the Tx to the blockchain (CMerkleTx), Tx w/ only info needed by the owner (CWalletTx), wallet Tx as represented in a TxOut (COutput), private wallet key (CWalletKey), a keystore extension w/ Tx/balance info (CWallet), keys allocated from the keypool (CReserveKey), account info (CAccount), internal accounting info (CAccountEntry), and many structs. The accounting stuff is more-or-less an abandoned concept from Core’s early days.

./src/wallet/wallet.h - See the CPP file.

./src/wallet/walletdb.cpp - Classes that provide key metadata (CKeyMetadata) and a derived class providing access to the wallet DB (wallet.dat) (CWalletDB).

./src/wallet/walletdb.h - See the CPP file.

./src/wallet/walletutil.cpp - Extra wallet functionality. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11466).

./src/wallet/walletutil.h - See the CPP file. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11466).

**./src/wallet/test** - Test code for the wallet.

~~./src/wallet/test/accounting\_tests.cpp~~ - [Wallet accounting entry tests](https://github.com/bitcoin/bitcoin/pull/1393). *[Moved here from ./src/test in 0.13](https://github.com/bitcoin/bitcoin/pull/7905) and [removed in 0.18](https://github.com/bitcoin/bitcoin/pull/14023)*.

./src/wallet/test/coinselector\_tests.cpp - Tests Core's coin selection algorithms. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10637).

./src/wallet/test/psbt\_wallet\_tests.cpp - Tests for [Partially Signed Bitcoin Transaction](https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki) wallet functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13557).

./src/wallet/test/rpc\_wallet\_tests.cpp - Internal RPC/JSON wallet unit tests. [*Moved here from ./src/test in 0.13*](https://github.com/bitcoin/bitcoin/pull/7905) and [*replaced with ./qa/rpc-tests/wallet-accounts.py in 0.14*](https://github.com/bitcoin/bitcoin/pull/8450).

./src/wallet/tests/wallet\_crypto\_tests.cpp - Various tests for the CTAES code. Ensures functionality matches OpenSSL, and that failures occur exactly like failures in OpenSSL. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7689) as a replacement for OpenSSL-dependent functionality, and [renamed in 0.17](https://github.com/bitcoin/bitcoin/pull/12895)*.

./src/wallet/test/wallet\_test\_fixture.cpp - Does some wallet test setup. Forces the wallet to use its own test fixtures, and not those for the rest of Core. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7905).

./src/wallet/test/wallet\_test\_fixture.h - See the CPP file.

./src/wallet/test/wallet\_tests.cpp - Test code for the wallet.

**./src/zmq** - Code supporting ØMQ. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6103).

./src/zmq/zmqabstractnotifier.cpp - Contains a pure virtual notifier class (CZMQAbstractNotifier).

./src/zmq/zmqabstractnotifier.h - See the CPP file.

./src/zmq/zmqconfig.h - Minimal file. Really seems useful only for the *zmqError()* prototype.

./src/zmq/zmqnotificationinterface.cpp - Has a derived notification interface class (CZMQNotificationInterface).

./src/zmq/zmqnotificationinterface.h - See the CPP file.

./src/zmq/zmqrpc.cpp - RPC call (*getzmqnotifications*) returning all active ZMQ notifications on the system. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13570).

./src/zmq/zmqrpc.h - See the CPP file. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13570).

./src/zmq/zmqpublishnotifier.cpp - Covers publishing for each covered event type. Has a derived virtual class (CZQAbstractPublishNotifier) that’s used as the base for the classes covering the four event types: block hash (CZMQPublishHashBlockNotifier), raw block (CZMQPublishRawBlockNotifier), Tx hash (CZMQPublishHashTransactionNotifier), and raw Tx (CZMQPublishRawTransactionNotifier).

./src/zmq/zmqpublishnotifier.h - See the CPP file.

**./test** - Core and related tests. Deals primarily with the Core binaries and how they respond to external input (flags, messages, etc.), not tests for internal source code. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

./test/config.ini.in - Sets, via Autoconfig wizardry, some variables to be used in ./qa/pull-tester/rpc-tests.ini, which is read by Python's *ConfigParser* module. Examples include enabling ØMQ tests. [*Replaced ./test/functional/config.ini.in in 0.15*](https://github.com/bitcoin/bitcoin/pull/10331).

./test/README.md - Explains how to run tests.

**./test/functional** - Regression tests to run and related helper files. [These tests focus on high-level external-facing functionality](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2014-July/006379.html), mostly related to RPC calls, but the tests also includes other test types (e.g., block serialization and various protocols). Also includes a set of tools that can be used to kick off Python-based tests, primarily based on Core's RPC functionality but including other test types based on external functionality. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/9956), with files moved from ./qa/pull-tester, and [reworked in 0.16](https://github.com/bitcoin/bitcoin/pull/11774) to give virtually all files one of seven prefixes: feature, interface, mempool, mining, p2p, rpc, wallet*.

./test/functional/.gitignore - Files for Git to ignore.

~~./test/functional/bipdersig.py~~ - [Confirms that the BIP 66 soft fork/switchover code works properly.](https://github.com/bitcoin/bitcoin/pull/5713) Uses BitcoinTestFramework. [Mike Hearn believes this is incomplete and removed it from Bitcoin XT](https://github.com/bitcoinxt/bitcoinxt/commit/8a4875b9ba9aacbeaead771a4c16ec3747c5a9df). [*Removed in 0.15*](https://github.com/bitcoin/bitcoin/pull/10695).

~~./test/functional/bip65-cltv~~.py - [Confirms that the BIP 65 soft fork/switchover code works properly.](https://github.com/bitcoin/bitcoin/pull/6351) Uses BitcoinTestFramework. [*Removed in 0.15*](https://github.com/bitcoin/bitcoin/pull/10695).

./test/functional/combine\_logs.py - A script that can aggregate multiple *bitcoind* log files when running ./test/functional/test\_runner.py, along with test\_framework.log for specific tests. Output can be text or HTML (see ./test/functional/combined\_log\_template.html). [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10017).

./test/functional/combined\_log\_template.html - HTML template for logs put together by ./test/functional/combine\_logs.py. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10017).
 
./test/functional/config.ini.in - Sets, via Autoconfig wizardry, some variables to be used in ./qa/pull-tester/rpc-tests.ini, which is read by Python's *ConfigParser* module. Examples include enabling ØMQ tests. *[Replaced ./qa/pull-tester/tests\_config.py.in in 0.15](https://github.com/bitcoin/bitcoin/pull/9657) and also [moved to ./test/config.ini.in in 0.15](https://github.com/bitcoin/bitcoin/pull/10331)*.

./test/functional/create\_cache.py - Helper code that initializes the blockchain cache used by the QA tests. It's meant to be called before any tests are run so that the blockchain is cached by [the *initialize\_chain* call in *BitcoinTestFramework* (the parent of *CreateCache*)](https://www.botbot.me/freenode/bitcoin-core-dev/2016-05-12/?msg=65947836&page=3). [*Assists with parallelized RPC tests, and added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7972).

./test/functional/example\_test.py - An example test that checks some RPC and P2P functionality. Meant to be copied and modified by people adding tests. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/10612).

./test/functional/feature\_assumevalid.py - Tests the *assumevalid* RPC call. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9484) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_bip68\_sequence.py - Tests BIP 68 functionality in the mempool. *[Added in 0.12.1](https://github.com/bitcoin/bitcoin/pull/7184) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

~~./test/functional/feature\_bip9-softforks.py~~ - Intended to test BIP 9 activation logic but only ever tested CSV activation, which is duplicated by ./test/functional/feature\_csv\_activation.py. *[Added in 0.12.1](https://github.com/bitcoin/bitcoin/pull/7648), [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774), and [removed in 0.17](https://github.com/bitcoin/bitcoin/pull/11818)*.

./test/functional/feature\_block.py - A partial port of [FullBlockTestGenerator.java](https://github.com/TheBlueMatt/test-scripts/blob/master/FullBlockTestGenerator.java), a file driven by BitcoinJ that generates test blockchains used to test/verify the handling of the blockchain in Core and various alternative implementations (e.g., BitcoinJ and BTCD). *[Added in 0.12](https://github.com/bitcoin/bitcoin/pull/6523) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/function/feature\_blocksdir.py - Checks to make sure the *blocksdir* command line parameter works as expected. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12653).

./test/functional/feature\_cltv.py - [Confirms that the BIP 65 soft fork/switchover code works properly in a P2P environment.](https://github.com/bitcoin/bitcoin/pull/6351) Uses *comptool*/ComparisonTestFramework. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/feature\_config\_args.py - Tests the config file and its arguments. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11883) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.
 
./test/functional/feature\_csv\_activation.py - Tests the activation logic of BIP 9 (aka "versionbits") and the consensus logic for BIPs 68, 112, and 113, all in a P2P environment. *[Added in 0.12.1](https://github.com/bitcoin/bitcoin/pull/7648) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.
 
./test/functional/feature\_dbcrash.py - Tests the *dbcrashratio* parameter to check the logic for recovering from a crash during a chainstate flush. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10148) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_dersig.py - [Confirms that the BIP 66 soft fork/switchover code works properly in a P2P environment.](https://github.com/bitcoin/bitcoin/pull/5981) Uses *comptool*/ComparisonTestFramework. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/feature\_fee\_estimation.py - [Tests the fee estimation code.](https://github.com/bitcoin/bitcoin/pull/3959) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/13049).

./test/function/feature\_help.py - Checks to make sure the *help* and *version* command line parameters work as expected. [*Added in 0.16.1*](https://github.com/bitcoin/bitcoin/pull/12843).

./test/function/feature\_includeconf.py - Checks to make sure the *includeconf* command line parameters work as expected. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10267).

./test/functional/feature\_logging.py - Tests the *debuglogfile* CL arg. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11781).

./test/functional/feature\_maxuploadtarget.py - Confirms that Core will work properly with the -maxuploadtarget option. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/feature\_minchainwork.py - Tests the *minimumchainwork* CL argument. *[Added in 0.15.1](https://github.com/bitcoin/bitcoin/pull/10357) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_notifications.py - Tests various CL flags related to notifications (e.g., *alertnotify*, *blocknotify*, and *walletnotify*). *[Moved from ./test/functional/forknotify.py in 0.16](https://github.com/bitcoin/bitcoin/pull/10941) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_nulldummy.py - Tests the P2P functionality with the [NULLDUMMY](https://github.com/bitcoin/bips/blob/master/bip-0147.mediawiki) softfork. *[Added in 0.13.1](https://github.com/bitcoin/bitcoin/pull/8636) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_proxy.py - [Various proxy tests for the *proxy*, *onion*, and *proxyrandomize* CL args.](https://github.com/bitcoin/bitcoin/pull/5911) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/feature\_pruning.py - [Tests block pruning functionality.](https://github.com/bitcoin/bitcoin/pull/5863) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/feature\_rpc.py - Tests the replace-by-fee functionality. *[Added in 0.12](https://github.com/bitcoin/bitcoin/pull/6871) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_reindex.py - [Tests reindexing with CheckBlockIndex functionality enabled, all on the CL.](https://github.com/bitcoin/bitcoin/pull/6012) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/feature\_segwit.py - Test for various bits of Segregated Witness functionality. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/8149) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_uacomment.py - Tests the *uacomment* CL flag. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11486) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/feature\_versionbits\_warning.py - Test for BIP 9 warning logic. *[Added in 0.12.1](https://github.com/bitcoin/bitcoin/pull/7575) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

~~./test/functional/forknotify~~.py - Tests the *alertnotify* CL flag for when a fork occurs. [*Moved to ./test/functional/notifications.py in 0.16*](https://github.com/bitcoin/bitcoin/pull/10941).

~~./test/functional/getblocktemplate\_proposals~~.py - Tests the "block proposal" functionality of the *getblocktemplate* RPC function (BIP 23). [*Replaced with ./test/functional/mining.py in 0.15*](https://github.com/bitcoin/bitcoin/pull/10190).

~~./test/functional/import-abort-rescan~~.py - Tests the *abortrescan* RPC functionality. *[Intended for 0.15](https://github.com/bitcoin/bitcoin/pull/10225) but [quickly pulled due to code flakiness](https://github.com/bitcoin/bitcoin/pull/10327)*.

./test/functional/interface\_bitcoin\_cli.cpp - Tests the *bitcoin-cli* binary, which can differ from the RPC interface. *[Added in 0.15.1](https://github.com/bitcoin/bitcoin/pull/10798) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/interface\_http.py - [Tests HTTP "keep-alive" functionality.](https://github.com/bitcoin/bitcoin/pull/5436) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/interface\_rest.py - Tests the REST interface functionality. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/interface\_zmq.py - Tests ØMQ RPC functionality. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

~~./test/functional/maxblocksinflight.py~~ - Tests whether a node is limiting the number of in-flight block requests. [Functionality reproduced by ./test/functional/sendheaders.py](https://github.com/bitcoin/bitcoin/pull/10023#issuecomment-293891932), so this file was [*removed in 0.15*](https://github.com/bitcoin/bitcoin/pull/10023).

./test/functional/mempool\_accept.py - Tests the acceptance of raw transactions into the mempool. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11742).

./test/functional/mempool\_limit.py - [Confirms that Core will work properly with the -maxmempool option](https://github.com/bitcoin/bitcoin/pull/7153).

./test/functional/mempool\_packages.py - [Tests the *descendantcount*, *descendantsize*, and *descendantfees* values from the *getrawmempool* RPC functionality.](https://github.com/bitcoin/bitcoin/pull/6654#issuecomment-141692820)

./test/functional/mempool\_persist.py - Tests the *persistmempool* CL flag, which, when false, causes Core to not read mempool.dat upon startup (i.e., the mempool isn't persistent across restarts). [Added in 0.15](https://github.com/bitcoin/bitcoin/pull/9966)

./test/functional/mempool\_reorg.py - [Tests the *invalidateblock* RPC functionality.](https://github.com/bitcoin/bitcoin/pull/5267) In particular, it makes sure that coins that were valid due toinvalidated blocks will no longer be valid.

./test/functional/mempool\_resurrect.py - [Confirms that a Tx in a block that was reorg'ed out is placed back in the mempool.](https://github.com/bitcoin/bitcoin/pull/5369) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/mempool\_spend\_coinbase.py - [Confirms that immature coinbase spends aren't allowed.](https://github.com/bitcoin/bitcoin/pull/5407) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/mining\_basic.py - Tests various bits of mining RPC functionality. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10190) as a replacement for ./test/functional/getblocktemplate\_proposals.py*. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/mining\_getblocktemplate\_longpoll.py - Tests the "long polling" functionality of the *getblocktemplate* RPC function (BIP 22). [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/mining\_prioritisetransaction.py - [Tests the *prioritisetransaction* RPC functionality.](https://github.com/bitcoin/bitcoin/pull/7147) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

~~./test/functional/nodehandling.py~~ - [Tests the *setban*, *listbanned*, and *disconnectnode* RPC functionality.](https://github.com/bitcoin/bitcoin/pull/6158) [*Moved to ./test/functional/disconnect\_ban.py in 0.15*](https://github.com/bitcoin/bitcoin/pull/10143).

./test/functional/p2p\_compactblocks.py - Tests various bits of CompactBlock functionality. *[Added in 0.13.1](https://github.com/bitcoin/bitcoin/pull/8418) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_disconnect\_ban.py - Tests the *setban*, *listbanned*, and *disconnectnode* RPC functionality. *[Moved from ./test/functional/nodehandling.py in 0.15](https://github.com/bitcoin/bitcoin/pull/10143) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_feefilter.py - Tests the *feefilter* P2P message. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7542) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_fingerprint.py - Tests whether or not a node won't return a stale block more than a month old. (Done to help prevent [fingerprinting](https://en.wikipedia.org/wiki/Device_fingerprint).) *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11113) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_invalid\_block.py - Tests P2P ability to process valid and invalid blocks received after requesting blocks. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/p2p\_invalid\_locator.py - Tests the maximum number of entries in a [locator](https://github.com/bitcoin/bitcoin/blob/e254ff5d53b79bee29203b965fca572f218bff54/src/primitives/block.h#L122-L125). [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13915).

./test/functional/p2p\_invalid\_tx.py - Checks to make sure that P2P "reject" mesages are properly sent and handled for transactions and blocks. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/p2p\_leak.py - Test for "leaky" P2P message behavior (e.g., messages received before a version is received, messages other than version/reject before sending a VERACK, etc.). *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9720) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_mempool.py - Test for *mempool* RPC command, in conjunction with disabled bloom filters. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/8078) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_node\_network\_limited.py - Testing for the [BIP 159](https://github.com/bitcoin/bips/blob/master/bip-0159.mediawiki)/NODE\_NETWORK\_LIMITED service bit (i.e., a node is signaling that it's pruned). *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11740) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_segwit.py - Test for external results of Segregated Witness functionality. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/8149) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_sendheaders.py - [Tests the *sendheaders* P2P message.](https://github.com/bitcoin/bitcoin/pull/7129) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/p2p\_timeouts.py - Test for peer disconnection logic (i.e., disconnect when no VERACKs are received within one minute). *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9715) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/p2p\_unrequested\_blocks.py - [Tests *AcceptBlock* functionality from ./src/main.cpp](https://github.com/bitcoin/bitcoin/pull/5875), which is basically how unrequested blocks are handled. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/README.md - Explains some the test\_framework subdirectory’s contents, along with some of the underlying technical details.

./test/functional/rpc\_bind.py - [Tests binding of RPC functionality to various interfaces.](https://github.com/bitcoin/bitcoin/pull/3695) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_blockchain.py - Tests the *gettxoutsetinfo* RPC functionality. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_createmultisig.py - Tests the *createmultisig* RPC functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13072).

./test/functional/rpc\_decodescript.py - Tests the *decodescript* RPC functionality. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_deprecated.py - Checks to see if deprecated RPC functions are actually marked as deprecated when used. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11031) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/rpc\_fundrawtransaction.py - Tests the *fundrawtransaction* RPC functionality. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_getblockstats.py - Tests the *getblockstats* RPC functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10757).

./test/functional/rpc\_getchaintips.py - Tests the *getchaintips* RPC functionality. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_help.py - Tests RPC help functionality. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/14020).

./test/functional/rpc\_invalidateblock.py - Tests the hidden *invalidateblock* RPC function. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

~~./test/functional/rpc\_listtransactions.py~~ - Tests the *listtransactions* RPC functionality. *[Renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774) and [moved to ./test/functional/wallet\_listtransactions in 0.17](https://github.com/bitcoin/bitcoin/pull/12953)*.

./test/functional/rpc\_named\_arguments.py - Tests support of JSON-RPC named args. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8811) (this file and the support for JSON-RPC named args) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/rpc\_net.py - A setnetworkactive() "smoke test." *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10077) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/rpc\_preciousblock.py - Tests the *preciousblock* RPC functionality. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/6996) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/rpc\_psbt.py - Tests the [Partially Signed Bitcoin Transaction](https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki) RPC functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13557).

./test/functional/rpc\_rawtransaction.py - [Tests reorg scenarios w/ a mempool that contain a Tx spending (direct or indirect) a coinbase Tx.](https://github.com/bitcoin/bitcoin/pull/5418) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_scantxoutset.py - Tests the *scantxoutset* RPC functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12196).

./test/functional/rpc\_signmessage.py - Tests signatures and verifications using the *signmessagewithprivkey* RPC call. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7953) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/rpc\_signrawtransaction.py - [Tests the *signrawtransaction* RPC functionality.](https://github.com/bitcoin/bitcoin/pull/5937) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_txoutproof.py - [Tests the generation and verification of merkle blocks.](https://github.com/bitcoin/bitcoin/pull/5199) In other words, it tests the *gettxoutproof* and *verifytxoutproof* RPC functionality, which relate to proofs that a given TXID is in a given block. (The proofs are serialized CMerkleBlock classes.) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_uptime.py - Tests the *uptime* RPC call (length of time *bitcoind* has been running). *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10400) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/rpc\_users.py - Tests to make sure that multiple *rpcuser* entries in bitcoin.conf will be properly handled by Core. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/rpc\_zmq.py - Tests the *getzmqnotifications* call. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13570).

./test/functional/test\_runner.py - Primary script that kicks off one or more tests found in ./test/functional. [*Added in 0.12*](https://github.com/bitcoin/bitcoin/pull/6616).

./test/functional/wallet\_abandontransaction.py - Tests the *abandontransaction* RPC call. *[Added in 0.12](https://github.com/bitcoin/bitcoin/pull/7312) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

~~./test/functional/wallet\_accounts.py~~ - Various RPC/JSON wallet unit tests. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8450) to replace ./src/wallet/test/rpc\_wallet\_tests.cpp, then [renamed to ./test/functional/wallet\_accounts.py in 0.16](https://github.com/bitcoin/bitcoin/pull/11774) and finally [renamed to ./test/functional/wallet\_labels.py in 0.17](https://github.com/bitcoin/bitcoin/pull/11536)*.

./test/functional/wallet\_address\_types.py - Tests various address types accepted (and not accepted) by Core. *[Added in 0.16](https://github.com/bitcoin/bitcoin/pull/11403) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_backup.py - Tests wallet backup functionality. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/wallet\_basic.py - Various wallet tests. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/wallet\_bumpfee.py - Tests the *bumpfee* RPC functionality. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8456) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_disable.py - Confirms that Core will work properly with the -disablewallet option. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/wallet\_disableprivatekeys.py - Confirms that Core will work properly with the -disableprivatekeys option for the wallet. [*Renamed in 0.17*](https://github.com/bitcoin/bitcoin/pull/9662).

./test/functional/wallet\_dump.py - Tests the *walletdump* RPC functionality. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/8417) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_encryption.py - Tests Core wallet's encryption functionality. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10551) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_fallbackfee.py - Tests Core wallet's replace-by-fee capabilities in conjunction with the *fallbackfee* CL arg. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/11882).

./test/functional/wallet\_groups.py - Tests Core's ability to combine UTXOs for one address and apply all of them towards one spend. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/12257).

./test/functional/wallet\_hd.py - Tests hierarchical deterministic qualities of the Core wallet. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/8309) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_import\_rescan.py - Tests the ability of the wallet to rescan after importing keys. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9331) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_importmulti.py - Tests the *importmulti* RPC functionality. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/7551) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_importprunedfunds.py - Tests the *importprunedfunds* and *removeprunedfunds* RPC calls. *[Added in 0.13](https://github.com/bitcoin/bitcoin/pull/7558) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_keypool.py - Wallet keypool tests that interact with wallet locking/unlocking. [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/wallet\_keytool\_topup.py - Tests Core's keypool refilling functionality (and the keys being marked as used when necessary) *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/11022) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_labels.py - Various RPC/JSON wallet unit tests. [*Renamed from ./test/functional/wallet\_labels.py in 0.17*](https://github.com/bitcoin/bitcoin/pull/11536).

./test/functional/wallet\_listreceivedby.py - [Tests the *getreceivedbyaddress* and *listreceivedbyaddress*  functionality.](https://github.com/bitcoin/bitcoin/pull/3960) [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/wallet\_listsinceblock.py - Tests the *listsinceblock* RPC functionality. In particular, it really wants to make sure that, if there's a reorg, the code will use the fork point as a reference, and not the relative position of a chain with less work. *[Added in 0.14](https://github.com/bitcoin/bitcoin/pull/9516) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_listtransactions.py - Tests the *listtransactions* wallet API. [*Moved from ./test/functional/rpc\_listtransactions in 0.17*](https://github.com/bitcoin/bitcoin/pull/12953).

./test/functional/wallet\_multiwallet.py - Tests multiwallet functionality. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10849) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_resendwallettransactions.py - Tests *resendwallettransactions* RPC functionality. *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/11000) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_txn\_clones.py - Confirms that, if a cloned Tx is malleated and sent on the network instead of the original Tx, the malleated Tx will be seen later and the original Tx ignored. *[Added in 0.12](https://github.com/bitcoin/bitcoin/pull/5881) and [renamed in 0.16](https://github.com/bitcoin/bitcoin/pull/11774)*.

./test/functional/wallet\_txn\_doublespend.py - [Tests double spend handling functionality](https://github.com/bitcoin/bitcoin/pull/5317). [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

./test/functional/wallet\_zapwallettxes.py - [Tests *zapwallettxes* functionality (CL arg)](https://github.com/bitcoin/bitcoin/pull/5612). [*Renamed in 0.16*](https://github.com/bitcoin/bitcoin/pull/11774).

**./test/functional/data** - Data for tests in the ./test/functional subdirectory. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10757).

./test/functional/data/rpc\_getblockstats.json - Data for the *getblockstats* test. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/10757).

./test/functional/data/rpc\_psbt.json - Data for the [Partially Signed Bitcoin Transaction](https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki) RPC functionality tests. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13557).

**./test/functional/test\_framework** - Non-test classes. *[Added in 0.11](https://github.com/bitcoin/bitcoin/pull/6097) as ./src/data/test\_framework and [moved to ./test/functional/test\_framework in 0.15](https://github.com/bitcoin/bitcoin/pull/9956)*.

./test/functional/test\_framework/\_\_init\_\_.py - Standard Python package init file.

./test/functional/test\_framework/address.py - Encodes and decodes Base58 P2PKH and P2SH addresses. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8499).

./test/functional/test\_framework/authproxy.py - [Enhanced version of *ServiceProxy* from *python-jsonrpc*](https://github.com/jgarzik/python-bitcoinrpc/blob/master/bitcoinrpc/authproxy.py). Used to handle RPC calls and such.

./test/functional/test\_framework/bignum.py - Helpers for ./test/functional/test\_framework/script.py.

~~./test/functional/test\_framework/blockstore.py~~ - Helper that implements disk-based block & Tx storage. Useful for replying to *getheaders* & *getdata*, and constructing a *getheaders* message. [*Removed in 0.17*](https://github.com/bitcoin/bitcoin/pull/11818).

./test/functional/test\_framework/blocktools.py - Helper functs for manipulating blocks & transactions.

~~./test/functional/test\_framework/comptool.py~~ - Compare two *bitcoind* instances. Useful for P2P tests. [*Removed in 0.17*](https://github.com/bitcoin/bitcoin/pull/11818).

./test/functional/test\_framework/coverage.py - [Code allowing for RPC call coverage.](https://github.com/bitcoin/bitcoin/pull/6804)

./test/functional/test\_framework/key.py - Wrapper around OpenSSL’s *EC\_Key* struct. [Fixes a crash in a regression test.](https://github.com/bitcoin/bitcoin/pull/6523#issuecomment-132381873)

./test/functional/test\_framework/messages.py - P2P message functionality. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11648)

./test/functional/test\_framework/mininode.py - [Basic P2P connectivity to a Bitcoin node via P2P.](https://github.com/bitcoin/bitcoin/pull/5981)

./test/functional/test\_framework/netutil.py - Generally useful network utilities.

./test/functional/test\_framework/script.py - Bitcoin script manipulation utilities.

./test/functional/test\_framework/segwit\_addr.py - Checks usage of Bech32 to encode SegWit addresses. [*Added in 0.16*](https://github.com/bitcoin/bitcoin/pull/11167).

./test/functional/test\_framework/siphash.py - [SipHash](https://en.wikipedia.org/wiki/SipHash) test utilities. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8418).

./test/functional/test\_framework/socks5.py - Dummy SOCKS5 server.

./test/functional/test\_framework/test\_framework.py - Basic framework references (plain-or-P2P/BitcoinTestFramework and, pre-0.17, multiple binary versions/ComparisonTestFramework). Includes descriptions of arguments recognized by test scripts. Referenced by ./qa/pull-tester/rpc-tests.py.

./test/functional/test\_framework/test\_node.py - Includes TestNode, a class responsible for all state related to a bitcoind node under test. It stores local state, is responsible for tracking the bitcoind process and delegates unrecognised messages to the RPC connection. [*Added in 0.15.1*](https://github.com/bitcoin/bitcoin/pull/10711).

./test/functional/test\_framework/util.py - Generally useful utilities.

./test/functional/test\_framework/wallet-dump.py - Tests the *dumpwallet* (and related) RPC functionality. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8417).

**./test/lint** - Files related to the *lint* test tool. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/check-doc.py - Checks if all command line args are documented. Used primarily for automated testing by the Core team. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/check-rpc-mappings.py - Checks if RPC commands are documented. Used primarily for automated testing by the Core team. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/commit-script-check.sh - A script that can use commands in a commit to verify that the code pre-commit matches what's in the commit when the commands are executed. Useful for things like mass changes (e.g., removing capitalization in all header files). *[Added in 0.15](https://github.com/bitcoin/bitcoin/pull/10189) and [moved to ./test/lint/commit-script-check.py in 0.17](https://github.com/bitcoin/bitcoin/pull/13281)*.

./test/lint/git-subtree-check.sh - [Verifies that subtree contents match upstream subtrees.](https://github.com/bitcoin/bitcoin/pull/5965) Must run from repo root. Currently useful for libsecp256k1 and LevelDB. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-all.sh - Generic shell script that executes all [lint](https://en.wikipedia.org/wiki/Lint_(software)) scripts in ./contrib/devtools. Used primarily for automated testing by the Core team. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-assertions.sh - Checks that assertions don't have side effects (e.g., variable assignments). [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/14088).

./test/lint/lint-circular-dependencies.sh - Checks for circular dependencies in the Core code. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13695).

./test/lint/lint-filenames.sh - A lint script that enforces the Core filename policy. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13450).

./test/lint/lint-format-strings.py - A lint script that checks the number of args in a variadic format string function and ensures that they match the number of format specifiers in the format string. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13705).

./test/lint/lint-format-strings.sh - A script that kicks off ./test/lint/lint-format-strings.py. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13705).

./test/lint/lint-include-guards.sh - A lint script that enforces the usage of [include guards](https://en.wikipedia.org/wiki/Include_guard) in C++ header files. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-includes.sh - A lint script that enforces Core's include guidelines (i.e., no duplicate header includes). [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-locale-dependence.sh - Checks for C/C++ calls that have [locale dependencies](https://www.math.hkbu.edu.hk/parallel/pgi/doc/pgC++_lib/stdlibug/sta_9169.htm) (e.g., *atoi*). [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13041).

./test/lint/lint-logs.sh - Checks for newline termination in log files. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-python.sh - A lint script that looks for unused Python imports. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-python-shebang.sh - A lint script that looks for missing Python [shebangs](https://en.wikipedia.org/wiki/Shebang_(Unix)). [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-python-utf8-encoding.sh - A lint script that ensures all Python files can be opened using UTF-8 or ASCII encoding. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13448).

./test/lint/lint-qt.sh - A lint script that ensures Core code uses Qt5-style [connect syntax](https://wiki.qt.io/New_Signal_Slot_Syntax). [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13529).

./test/lint/lint-shell.sh - A lint script that looks for [shellcheck](https://www.shellcheck.net/) warnings in shell scripts (i.e., shell script bugs). [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-shell-locale.sh - A lint script that enforces the usage of ["LC_ALL=C"](https://unix.stackexchange.com/questions/87745/what-does-lc-all-c-do) in all shell scripts. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13454).

./test/lint/lint-spelling.ignore-words.txt - A list of words to ignore when looking for spelling errors in ./test/list/lint-spelling.sh. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13954).

./test/lint/lint-spelling.sh - A lint script that throws up warnings on misspelled words, using [*codespell*](https://github.com/codespell-project/codespell) to find the words. [*Added in 0.18*](https://github.com/bitcoin/bitcoin/pull/13954).

./test/lint/lint-tests.sh - A lint script that enforces the naming convention of files in ./src/test/ and ./src/wallet/test/. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/lint-whitespace.sh - A lint script that looks for trailing whitespace added by new commits. [*Moved from ./contrib/devtools in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

./test/lint/README.md - Explains some of the tests and their functionality. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13281).

**./test/util** - Test-related utility files. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

~~./test/util/bctest.py~~ - [Support code for *bitcoin-tx* binary test](https://github.com/bitcoin/bitcoin/pull/4624). *[Moved from ./src/test/bctest.py in 0.15](https://github.com/bitcoin/bitcoin/pull/9956) and [quickly deleted and moved into ./test/util/bitoin-util-test.py in 0.15](https://github.com/bitcoin/bitcoin/pull/10331)*.

./test/util/bitcoin-util-test.py - [Kicks off *bitcoin-tx* binary test](https://github.com/bitcoin/bitcoin/pull/4624). [*Moved from ./src/test/bitcoin-util-test.py in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

./test/util/buildenv.py.in - [Helps allow Python tests to run on Windows](https://github.com/bitcoin/bitcoin/pull/5014). [*Moved from ./src/test/buildenv.py.in in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956).

./test/util/rpcauth-test.py - RPC authentication tests. [*Added in 0.17*](https://github.com/bitcoin/bitcoin/pull/13056).

**./test/util/data** - Data for unit tests in ./test/functional. [*Added in 0.15*](https://github.com/bitcoin/bitcoin/pull/9956), consisting of files moved from ./src/test/data.

./test/util/data/bitcoin-util-test.json - Test data for the *bitcoin-tx* binary test. [Used by ./src/test/bitcoin-util-test.py](https://github.com/bitcoin/bitcoin/pull/4624) to trigger tests.

./test/util/data/blanktx.json - Test data for the *bitcoin-tx* binary test. Checks the results of creating a blank v1 Tx. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/blanktxv1.hex - Test data for the *bitcoin-tx* binary test. [Used by ./test/util/data/bitcoin-util-test.json](https://github.com/bitcoin/bitcoin/pull/4624) with *bitcoin-tx -create -nversion=1* to ensure that a blank v1 transaction is correct. [*Changed from ./src/test/data/blanktx.hex to ./src/test/data/blanktxv1.hex in 0.14*](https://github.com/bitcoin/bitcoin/pull/7562).

./test/util/data/blanktxv2.hex - Test data for the *bitcoin-tx* binary test. [Used by ./test/util/data/bitcoin-util-test.json](https://github.com/bitcoin/bitcoin/pull/4624) with *bitcoin-tx -create -nversion=1* to ensure that a blank v1 transaction is correct. [*Changed from ./src/test/data/blanktx.hex to ./src/test/data/blanktxv1.hex in 0.14*](https://github.com/bitcoin/bitcoin/pull/7562).

./test/util/data/blanktxv2.json - Test data for the *bitcoin-tx* binary test. Checks the results of creating a blank v2 Tx. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/7562).

./test/util/data/README.md - Mentions that this is data for various tests.

./test/util/data/tt-delin1-out.hex - *bitcoin-tx -delin=1* test data used for output comparison. [Used by ./test/util/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4733)

./test/util/data/tt-delin1-out.json - *bitcoin-tx -json -delin=1* test data used for output comparison. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/tt-delout1-out.hex - *bitcoin-tx -delout=1* test data used for output comparison. [Used by ./test/util/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4733)

./test/util/data/tt-delout1-out.json - *bitcoin-tx -json -delout=1* test data used for output comparison. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/tt-locktime317000-out.hex - *bitcoin-tx -lockout=317000* test data used for output comparison. [Used by ./test/util/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4733)

./test/util/data/tt-locktime317000-out.json - *bitcoin-tx -json -lockout=317000* test data used for output comparison. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/tx394b54bb.hex - *bitcoin-tx* input test data. [Used by ./test/util/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4733)

./test/util/data/txcreate1.hex - *bitcoin-tx -create *loads of flags** input test data. [Used by ./test/util/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4733)

./test/util/data/txcreate1.json - *bitcoin-tx -json -create *loads of flags** input test data. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/txcreate2.hex - *bitcoin-tx -create outscript=0:* (i.e., null scriptPubKey) test data used for output comparison. [Used by ./test/util/data/bitcoin-util-test.json.](https://github.com/bitcoin/bitcoin/pull/4909)

./test/util/data/txcreate2.json - *bitcoin-tx -json -create outscript=0:* (i.e., null scriptPubKey) test data used for output comparison. Empty when committed. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/txcreatedata\_seq0.hex - Output comparison data for *bitcoin-tx* (RPC) transaction creation. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7957).

./test/util/data/txcreatedata\_seq0.json - Output comparison data for *bitcoin-tx* (RPC-JSON) transaction creation. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/txcreatedata\_seq1.hex - Output comparison data for *bitcoin-tx* (RPC) transaction creation. [*Added in 0.13*](https://github.com/bitcoin/bitcoin/pull/7957).

./test/util/data/txcreatedata\_seq1.json - Output comparison data for *bitcoin-tx* (RPC-JSON) transaction creation. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/txcreatedata1.hex - [Data for tests regarding data-based outputs (OP\_RETURN) from *bitcoin-tx*](https://github.com/bitcoin/bitcoin/pull/6346).

./test/util/data/txcreatedata1.json - Data for tests regarding data-based outputs (OP\_RETURN) from *bitcoin-tx* in JSON mode. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/txcreatedata2.hex - [Data for tests regarding data-based outputs (OP\_RETURN) from *bitcoin-tx*](https://github.com/bitcoin/bitcoin/pull/6346).

./test/util/data/txcreatedata2.json - Data for tests regarding data-based outputs (OP\_RETURN) from *bitcoin-tx* in JSON mode. [*Added in 0.13.1*](https://github.com/bitcoin/bitcoin/pull/8829).

./test/util/data/txcreatemultisig1.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2PKH output. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatemultisig1.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2PKH out. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatemultisig2.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2PKH output in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatemultisig2.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2PKH output in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatemultisig3.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2WSH output. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatemultisig3.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2WSH output. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatemultisig4.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2WSH output in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatemultisig5.json - Expected output result (JSON) when attempting in *bitcoin-tx* to use uncompressed public keys in output adds. (It should fail for SegWit outputs and succeed for "legacy" outputs.) [*Added in 0.15.1*](https://github.com/bitcoin/bitcoin/pull/11377).

./test/util/data/txcreatemultisig4.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a 2-of-3 multisig Tx P2WSH output in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreateoutpubkey1.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a Tx P2PK output. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreateoutpubkey1.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a Tx P2PK output. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreateoutpubkey2.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WPK output. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreateoutpubkey2.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WPK output. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreateoutpubkey3.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WPK output in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreateoutpubkey3.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WPK output in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript1.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a Tx P2PKH output with a single script (OP\_DROP). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript1.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a Tx P2PKH output with a single script (OP\_DROP). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript2.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a Tx P2PKH output with a single script (OP\_DROP) in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript2.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a Tx P2PKH output with a single script (OP\_DROP) in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript3.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WSH output with a single script (OP\_DROP). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript3.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WSH output with a single script (OP\_DROP). [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript4.hex - Expected output result (hex) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WSH output with a single script (OP\_DROP) in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatescript4.json - Expected output result (JSON) when using *bitcoin-tx* to generate, using some given input data, a Tx P2WSH output with a single script (OP\_DROP) in P2SH form. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/8883).

./test/util/data/txcreatesignv1.hex - *bitcoin-tx -create *loads of flags** input test data. [Used by ./test/util/data/bitcoin-util-test.json](https://github.com/bitcoin/bitcoin/pull/5528) to create a v1 Tx with a signle input and output, and then sign the Tx. [A later change was made to fix some issues](https://github.com/bitcoin/bitcoin/pull/6390). [*Changed from ./src/test/data/txcreatesign.hex to ./src/test/data/txcreatesignv1.hex in 0.14*](https://github.com/bitcoin/bitcoin/pull/7562).

./test/util/data/txcreatesignv1.json - *bitcoin-tx -json -create *loads of flags** input test data. Used to create a v2 Tx with a signle input and output, and then sign the Tx, with the output in json. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/7562).

./test/util/data/txcreatesignv2.hex - *bitcoin-tx -create *loads of flags** input test data. Used by ./test/util/data/bitcoin-util-test.json to create a v2 Tx with a signle input and output, and then sign the Tx. [*Added in 0.14*](https://github.com/bitcoin/bitcoin/pull/7562).
