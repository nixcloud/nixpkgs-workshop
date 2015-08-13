# nix programming / language introduction

a good start into nix/nixos is reading the wiki at [1] as it provides links to all important documentations. 

question: find out what the difference between nix/nixos/nixpkgs documentation is. 

# nixpkgs construction

all packages and services are packaged inside nixpkgs, so we need a copy of that. you need

1. go to https://github.com/nixos/nixpkgs
2. clone nixpkgs
3. cd nixpkgs


* pkgs
* nixos


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

