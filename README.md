# nix related workshops

welcome to the second `workshop on the cccamp2015`, after we've been using `nix-shell` to instantiate custom environments with toolchains for 
developing software we are now going into `nixpkgs` and how software is packaged:

* https://events.ccc.de/camp/2015/wiki/Session:NixOS
* https://nixos.org/wiki/NixOS_Chaos_Communication_Camp_2015#workshop:_nixpkgs
* https://github.com/nixcloud/nixpkgs-workshop

so, let's get started...

# nix programming / language introduction

a good start into nix/nixos is reading the wiki at [1] as it provides links to all important documentations. 

question: find out what the difference between nix/nixos/nixpkgs documentation coverage is. 

# nixpkgs construction

all packages and services are packaged inside nixpkgs, so we need a copy of that.
You need to check them out from github:

1. go to https://github.com/nixos/nixpkgs and get the url required to clone 
this repository.

2. switch to your local machine and clone the repository with:

        git clone 'url you just looked up'

    The problem now is that we have the newest version of the NIXPKGS. This  means we are ahead of the nixchannel. This can result in a rebuild of many packages. To avoid this we are going to get the same NIXPKGS version as it is used on our local machine. Doing so enables us to recieve packages from the binary cache.

3. move into the nixpkgs directory:

        cd nixpkgs

4. get your local nixversion:

        nixos-version

    Your result should loock similar to this:

        15.07pre66213.9d5508d (Dingo)

5. Now we can checkout the same version from git:

        git checkout 9d5508d
        git checkout -b 'fix/pkg-name-update'


the directory listing `ls -la` now lists several directories:

* lib
  a bunch of library functions, see `lib/attrsets.nix`, there are lots of examples included on how to use the functions provided for attribute sets, in short; attrsets

* pkgs
  contains all the software (or packages) in form of nix-expressions called `default.nix`. see `pkgs/top-level` and especially `pkgs/top-level/all-packages.nix` and 

* nixos
  contains `nixos/modules/` which represents all services which can be configured on nixos, see http://nixos.org/nixos/options.html for possible configuration values. 
  `nixos/tests` also provides unit tests which will be covered in the https://nixos.org/wiki/NixOS_Chaos_Communication_Camp_2015#workshop:_nixos_unit_tests workshop.

question: `nix-env -I nixpkgs=/your/directory/nixpkgs -qaP` uses your local checkout instead of the one provided by nix-channel.

## packages and options
* http://nixos.org/nixos/packages.html
* http://nixos.org/nixos/options.html

`nix-env -qaP` shows a list of packags, read http://nixos.org/nix/manual/#sec-expression-syntax and look for two important things: `attribute` and `name`.

question: what is the difference between an `attribute` and a `name`. issue this command: `nix-env -qaP | grep qt4` and use `nix-shell` to 
get a custom environment with `nixos.pkgs.qt5Full` inside. 

note: if you are in your qt5Full environment issue `qmake --version` to verify that it is working.

now go to your `nixpkgs` checkout 



http://nixos.org/nixpkgs/manual/#chap-functions

# understanding how dependencies in nixos work
# deploying your custom software using nix-env/nixos-rebuild/nix-shell

# documentation

* [1] http://wiki.nixos.org
* [2] http://nixos.org/nix/manual/
* [3] http://nixos.org/nixos/manual/
* [4] http://nixos.org/nixpkgs/manual/
* [5] https://nixos.org/wiki/Cheatsheet

