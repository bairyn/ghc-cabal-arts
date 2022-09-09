# Overview

This is the Archlinux source package (in the sense of the PKGBUILD file) for
‘ghc-cabal-arts’, a package that provides a standard GHC and cabal-install
setup but with dynamic and static files, so that users can build additional
packages without having to also update the default configuration to build
dynamically only; but also that includes the ‘fix-dynamic-deps’ patchset (cabal
pull-request ID 8461), to further enhance the build by tracking static vs.
dynamic build artifacts in ghc-pkg InstalledPackageInfo's (requires a patched
ghc-pkg too for this function to be enabled, from ghc.git) and managing these
fields when figuring out dependencies.

The patchset can be found here: <https://github.com/haskell/cabal/pull/8461>.

This package is intended to fix errors of the sort:

```
[1 of 1] Compiling Main             ( Main.hs, ../setup.dist/work/depender/dist/build/depender/depender-tmp/Main.o )

Main.hs:3:1: error:
    Could not find module `Dynamic'
    There are files missing in the `dynamic-1.0' package,
    try running 'ghc-pkg check'.
    Use -v (or `:set -v` in ghci) to see a list of the files searched for.
  |
  | import qualified Dynamic (number)
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```
