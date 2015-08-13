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

5. Now we can checkout the same version from git using the last part of the version number. (In the example it is 9d5508d, you should replace it with your nixos-version number).

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

# example
We want to extend the nano pkg with syntax highliting for '.nix' files. This requires to include the 'nix.nanorc' file into the installation path of nixos. 

1. Navigate into your nixpkgs directory and find the directory which holds all nano related files. At the moment there is only the 'default.nix'. Add the 'nix.nanorc' from this repository to the nano directory.

2. Now we need to adjust the 'default.nix' in a way that adds the 'nix.nanorc' to the installation folder. Open the 'default.nix' with an editor of your choise. We now 
add a 'hook' that enables us to acces the 'nix.nanorc' after the installation. Add the following code to your 'default.nix'.

        hook = ./nix.nanorc;

3. Add another attribute with the name 'postInstall'. Within this Attribute we define what should happen after nano is installed. In our case we want to copy the 
'nix.nanorc' into the 'share/nano/' directory within the installation folder.  

    Write a small script (within the default.nix) that copies the nix.nanorc into the 'share/nano/' directory. You can embed some nixvariables into the string. For 
example $out ist the installation path of nano and ${hook} is the nix.nanorc file.

        postInstall = '' TODO '';


4. install nano 

5. Enjoy the new syntaxhighliting. (If you are working on your own machine you have to enable syntaxhighliting first. You can do this by adding 'programs.nano.nanorc 
= "include ${pkgs.nano}/share/nano/*.nanorc"' to your configuration.nix)

http://nixos.org/nixpkgs/manual/#chap-functions

# understanding how dependencies in nixos work
# deploying your custom software using nix-env/nixos-rebuild/nix-shell

# documentation

* [1] http://wiki.nixos.org
* [2] http://nixos.org/nix/manual/
* [3] http://nixos.org/nixos/manual/
* [4] http://nixos.org/nixpkgs/manual/
* [5] https://nixos.org/wiki/Cheatsheet

