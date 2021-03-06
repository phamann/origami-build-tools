# Troubleshooting Origami Build Tools

Different common issues encountered when using OBT organized by the different tasks.

## `install`

### Installing Ruby

* Macs typically ship with Ruby by default, but:
	- If you get a `Gem::FilePermissionError` error, you need to [install a ruby version manager](http://stackoverflow.com/questions/19579392/installing-gem-fails-with-permissions-error).
	- To [install rbenv](https://github.com/sstephenson/rbenv#homebrew-on-mac-os-x) you first need to [install homebrew](http://brew.sh/).
	- Once you've installed rbenv you need to [install ruby](https://github.com/sstephenson/rbenv/#installing-ruby-versions).
		- Note: rbenv needs a bit of post-install setup. If you install with homebrew, also do steps 2 and 3 of the [Basic GitHub Checkout](https://github.com/sstephenson/rbenv/#basic-github-checkout) section.

### Error `Unable to download data from https://rubygems.org/`

If you receive an error specifying `Unable to download data from https://rubygems.org/ - SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://api.rubygems.org/specs.4.8.gz)` you'll need to manually update your gem package using the directions in [this gist](https://gist.github.com/luislavena/f064211759ee0f806c88).

### Error `While executing gem ... (Gem::FilePermissionError)`

When installing [SCSS-Lint](https://github.com/causes/scss-lint), depending on how permissions are set on your machine, OBT might fail and return:

>While executing gem ... (Gem::FilePermissionError).
>You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.

This can be fixed by following the [Installing Ruby steps](#installing-ruby) mentioned above.

If the error still occurs, run the command manually by prefixing sudo to it. It's the following command (substituting the version number by the one mentioned [here](https://github.com/Financial-Times/origami-build-tools/#install)):

```bash
sudo gem install scss-lint -v 0.35.0
```

### Error `npm ERR! argv "/usr/local/bin/node" "/usr/local/bin/npm" "install" "-g" "bower" "--quiet"`

When installing [bower](https://bower.io), depending on how permissions are set on your machine, OBT might fail and return something like this:

>npm ERR! Darwin 14.3.0
>npm ERR! argv "/usr/local/bin/node" "/usr/local/bin/npm" "install" "-g" "bower" "--quiet"
>npm ERR! node v0.12.2
>npm ERR! npm  v2.1.6
>npm ERR! path /usr/local/lib/node_modules/bower
>npm ERR! code EACCES
>npm ERR! errno -13
>
>npm ERR! Error: EACCES, unlink '/usr/local/lib/node_modules/bower'
>npm ERR!     at Error (native)
>npm ERR!  { [Error: EACCES, unlink '/usr/local/lib/node_modules/bower']
>npm ERR!   errno: -13,
>npm ERR!   code: 'EACCES',
>npm ERR!   path: '/usr/local/lib/node_modules/bower' }
>npm ERR!
>npm ERR! Please try running this command again as root/Administrator.

The command can be ran manually prefixing sudo to it. It's the following command (substituting the version number by the one mentioned [here](https://github.com/Financial-Times/origami-build-tools/#install)):

```bash
sudo npm install -g bower@^1.3.1
```

### Warning `Origami registry is not configured in a .bowerrc file`

Origami modules are listed on Origami's custom Bower registry, and aren't available to the global, public one. Custom registries can be added to a `.bowerrc` configuration file located in your home directory. To create a `.bowerrc` configuration file now, run::

```bash
echo '{"registry":{"search":["http://registry.origami.ft.com","https://bower.herokuapp.com"]}}' > ~/.bowerrc
```
