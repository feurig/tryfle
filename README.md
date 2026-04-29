# tryfle A look at flet for building cross platform apps

## Flet on macos (tahoe)

Installing and trying flet on macos was relatively painless.

### flet run on macos
``` sh
git clone git@github.com:feurig/tryfle.git
cd tryfle
flet create --project-name=hello
flet run
```

![fletrunning](docs/images/flet-run.jpg)

Which is pretty damned cool!

### flet build for macos

We are supposed to be able to build binaries so....

```sh
flet build macos -v
```

#### fails

flet build uses a pile of google provided ruby named flutter. One of its dependencies is cocoapods. Which doesn't play well with the arcane version of ruby that is still the default on macos tahoe.

And installing ruby 3 or 4 on macos is just a pile.

```sh
sudo gem install cocoapods
gem install ffi -v 1.17.4
sudo gem install ffi -v 1.17.4
# FAILS !!!!
brew install ruby
brew install ruby3
brew install ruby@3.4
type ruby
which ruby
ruby --version
brew install ruby
brew install ruby@3.4
echo "eval $(/opt/homebrew/bin/brew shellenv)" >> ~/.zprofile
eval $(/usr/local/bin/brew shellenv)
# FAILS !!!! then some googles....
brew install rbenv
/usr/local/bin/rbenv install --list-all
brew show ruby
brew info ruby
/usr/local/bin/rbenv install 4.0.0
# FAILS !!!!
/usr/local/bin/rbenv install 3.3.11
# FAILS !!!!
brew install openssl
brew reinstall openssl
/usr/local/bin/rbenv install 4.0.0
# FAILS !!!!
brew reinstall libopenssl
brew info ruby
/usr/local/bin/rbenv install 4.0.3
# FAILS !!!! ...more googles...
brew install openssl@1.1
export RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@1.1)"\nrbenv install 3.0.6
export RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@3)"\n\nrbenv install 3.3.3
# FAILS !!!!
```

#### DOH! homebrew has a cocoapods

```sh
brew install cocoapods
brew link --overwrite cocoapods
```

#### Neeto!!!

![hello app](docs/images/hello-app.jpg)

#### Pushing the mac a little further.

So for fun I found a CC hello world icon ![icon](src/assets/icon.png) 

and replaced the flet one.
The [license with the attribution](src/assets/LICENSE.md) is
is in the repo with under src/assets.

```sh
feurig@pj tryfle % flet build macos -v
[19:39:58] Run subprocess: ['/Users/feurig/flutter/3.41.4/bin/flutter', '--version',
...
╭────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Successfully built your macOS bundle! 🥳 Find it in build/macos directory. 📁                  │
╰────────────────────────────────────────────────────────────────────────────────────────────────╯
feurig@pj tryfle % rm -rf ~/Applications/hello.app
feurig@pj tryfle % mv build/macos/hello.app ~/Applications
```

The flet icon still shows up still shows up in the task bar.
But it looks and feels more like a mac app.

![new icon](docs/images/hello-app2.jpg)

### cross compiling on the mac (FAIL)

YOU ARE HERE.

### cross compiling on debian (FAIL)

AND HERE

### cross compiling on rasberian (partial FAIL)

AND HERE

## References

https://dev.to/flet/tutorial-build-and-package-a-multi-platform-desktop-app-in-python-3ncc