brew(1) -- The missing package manager for OS X
===============================================

## SYNOPSIS

`brew` [--verbose|-v] command [options] [formula] ...  
`brew` [--version|-v]

## DESCRIPTION

Homebrew is the easiest and most flexible way to install the UNIX tools Apple
didn't include with OS X.

## OPTIONS
  * `-v`, `--verbose` command [options] [formula] ...:
    Prints extra, command-specific debugging information.
    Note that `brew -v` by itself is the same as `brew --version`.

## ESSENTIAL COMMANDS

For the full command list, see the COMMANDS section.

  * `install` <formula>:
    Install <formula>.

  * `remove` <formula>:
    Uninstall <formula>.

  * `update`:
    Fetch the newest version of Homebrew from GitHub using `git`(1).

  * `list`:
    List all installed formulae.

  * `search`, `-S` <text>|/<text>/:
    Perform a substring search of formula names for <text>. If <text> is
    surrounded with slashes, then it is interpreted as a regular expression.
    If no search term is given, all available formula are displayed.

## COMMANDS

  * `audit [--strict]` [<formulae>]:
    Check <formulae> for Homebrew coding style violations. This should be
    run before submitting a new formula.

    If no <formulae> are provided, all of them are checked.

    If `--strict` is passed, perform additional stricter checks that may not need
    to be fixed before submitting.

    `audit` exits with a non-zero status if any errors are found. This is useful,
    for instance, for implementing pre-commit hooks.

  * `cat` <formula>:
    Display the source to <formula>.

  * `cleanup [--force]` [<formula>]:
    For all installed or specific formulae, remove any older versions from the
    cellar. By default, does not remove out-of-date keg-only brews, as other
    software may link directly to specific versions.

    If `--force` is passed, remove out-of-date keg-only brews as well.

  * `create [--no-fetch]` <URL>:
    Generate a formula for the downloadable file at <URL> and opens it in
    $EDITOR. Homebrew will attempt to automatically derive the formula name
    and version, if it fails, you'll have to make your own template. I suggest
    copying wget's.

    If `--no-fetch` is passed, Homebrew will not download <URL> to the cache and
    will thus not add the MD5 to the formula for you.

  * `deps [--1]` <formula>:
    Show <formula>'s dependencies.

    If `--1` is passed, only show dependencies one level down, instead of
    recursing.

  * `doctor`:
    Check your system for potential problems.

  * `edit`:
    Open all of Homebrew for editing in TextMate.

  * `edit` <formula>:
    Open <formula> in $EDITOR.

  * `fetch [--force] [-v] [--HEAD] [--deps]` <formulae>:
    Download the source packages for the given <formulae>.
    For tarballs, also print MD5 and SHA1 checksums.

    If `--HEAD` is passed, download the HEAD versions of <formulae> instead. `-v`
    may also be passed to make the VCS checkout verbose, useful for seeing if
    an existing HEAD cache has been updated.

    If `--force` is passed, remove a previously cached version and re-fetch.

    If `--deps` is passed, also download dependencies for any listed <formulae>.

  * `home`:
    Open Homebrew's own homepage in a browser.

  * `home` <formula>:
    Open <formula>'s homepage in a browser.

  * `info` <formula>:
    Display information about <formula>.

  * `info --github` <formula>:
    Open a browser to the GitHub History page for formula <formula>.

    To view formula history locally: `brew log -p <formula>`.

  * `info` <URL>:
    Print the name and version that will be detected for <URL>.

  * `install [--force] [--debug] [--ignore-dependencies] [--use-llvm] [--use-gcc] [--HEAD]` <formula>:
    Install <formula>.

    <formula> is usually the name of the formula to install, but may also be
    the URL for an arbitrary formula.

    If `--force` is passed, will install <formula> even if it is already
    installed. This can be used to re-install a formula without removing
    it first.

    If `--debug` is passed and brewing fails, open a shell inside the
    temporary folder used for compiling.

    If `--ignore-dependencies` is passed, skip installing any dependencies of
    any kind. If they are not already present, the formula will probably fail
    to install.

    If `--use-llvm` is passed, attempt to compile using the LLVM front-end to GCC.
    *NOTE*: Not all formulae will build with LLVM.

    If `--use-gcc` is passed, attempt to compile using GCC. This is useful for
    systems whose default compiler is LLVM-GCC.

    If `--HEAD` is passed, and <formula> defines it, install the HEAD version,
    aka master, trunk, unstable, dev.

    To install a newer version of HEAD use
    `brew rm <foo> && brew install --HEAD <foo>`
    or `brew install --force --HEAD <foo>`.

  * `install --interactive [--git]` <formula>:
    Download and patch <formula>, then open a shell. This allows the user to
    run `./configure --help` and otherwise determine how to turn the software
    package into a Homebrew formula.

    If `--git` is passed, Homebrew will create a Git repository, useful for
    creating patches to the software.

  * `ln`, `link` <formula>:
    Symlink all of <formula>'s installed files into the Homebrew prefix. This
    is done automatically when you install formula, but can be useful for DIY
    installations.

  * `list`:
    List all installed formulae.

  * `list` <formula>:
    List the installed files for <formula>.

  * `log [git-log-options]` <formula> ...:
    Show the git log for the given formulae. Options that `git-log`(1)
    recognizes can be passed before the formula list.

  * `man`:
    Regenerate this man page using [`ronn`][ronn]. See `man brew-man` for details.

  * `missing` [<formulae>]:
    Check the given <formulae> for missing dependencies.

    If no <formulae> are given, check all installed brews.

  * `options [--compact] [--all]` <formula>:
    Display install options specific to <formula>.

    If `--compact` is passed, show all options on a single line separated by
    spaces.

    If `--all` is passed, show options for all formulae.

  * `outdated`:
    Show formula that have an updated version available.

  * `prune`:
    Remove dead symlinks from the Homebrew prefix. This is generally not
    needed, but can be useful when doing DIY installations.

  * `rm`, `remove`, `uninstall [--force]` <formula>:
    Uninstall <formula>.

    If `--force` is passed, and there are multiple versions of <formula>
    installed, delete all installed versions.

  * `search`, `-S` <text>|/<text>/:
    Perform a substring search of formula names for <text>. If <text> is
    surrounded with slashes, then it is interpreted as a regular expression.
    If no search term is given, all available formula are displayed.

  * `search --macports`|`--fink` <text>:
    Search for <text> on the MacPorts or Fink package search page.

  * `server`:
    Start a local web app that lets you browse available formulae, similar
    to `gem server`. Requires [`sinatra`][sinatra].

  * `test` <formula>:
    A few formulae provide a test method. `brew test <formula>` runs this
    test method. There is no standard output or return code, but it should
    generally indicate to the user if something is wrong with the installed
    formula.

    Example: `brew install jruby && brew test jruby`

  * `unlink` <formula>:
    Unsymlink <formula> from the Homebrew prefix. This can be useful for
    temporarily disabling a formula: `brew unlink foo && commands && brew link foo`.

  * `update`:
    Fetch the newest version of Homebrew from GitHub using `git`(1).

  * `uses [--installed]` <formula>:
    Show the formulas that specify <formula> as a dependency. The list is
    not recursive; only one level of dependencies is resolved.

    If `--installed` is passed, only lists installed formulae.

  * `--cache`:
    Display Homebrew's download cache. *Default:* `~/Library/Cache/Homebrew`

  * `--cache` <formula>:
    Display the file or folder used to cache <formula>.

  * `--cellar`:
    Display Homebrew's Cellar path. *Default:* `/usr/local/Cellar`

  * `--cellar` <formula>:
    Display the location in the cellar where <formula> would be installed,
    without any sort of versioned folder as the last path.

  * `--config`:
    Show Homebrew and system configuration useful for debugging. If you file
    a bug report, you will likely be asked for this information if you do not
    provide it.

  * `--prefix`:
    Display Homebrew's install path. *Default:* `/usr/local`

  * `--prefix` <formula>:
    Display the location in the cellar where <formula> is or would be installed.

  * `--repository`:
    Display where Homebrew's `.git` folder is located. For standard installs,
    the `prefix` and `repository` are the same folder.

  * `-v`, `--version`:
    Print the version number of brew to standard error and exit.

## EXTERNAL COMMANDS

Homebrew allows external commands to be defined by putting a +x file named
`brew-<cmdname>` or `brew-<cmdname>.rb` on the PATH. This will cause Homebrew
to recognize `brew cmdname`.

Some sample commands ship with Homebrew and are enabled by default.

    $ ls `brew --repository`/Library/Contributions/examples



## ENVIRONMENT

  * HOMEBREW\_DEBUG:
    If set, instructs Homebrew to always assume `--debug` when running
    commands.

  * HOMEBREW\_DEBUG\_INSTALL:
    When `brew install -d` or `brew install -i` drops into a shell,
    `HOMEBREW_DEBUG_INSTALL` will be set to the name of the formula being
    brewed.

  * HOMEBREW\_DEBUG\_PREFIX:
    When `brew install -d` or `brew install -i` drops into a shell,
    `HOMEBREW_DEBUG_PREFIX` will be set to the target prefix in the Cellar
    of the formula being brewed.

  * HOMEBREW\_EDITOR:
    If set, Homebrew will use this editor when editing a single formula, or
    several formulae in the same folder.

    *NOTE*: `brew edit` will open all of Homebrew as discontinuous files and
    folders. TextMate can handle this correctly in project mode, but many
    editors will do strange things in this case.

  * HOMEBREW\_KEEP\_INFO:
    If set, Homebrew will not remove files from `share/info`, allowing them
    to be linked from the Cellar.

  * HOMEBREW\_SVN:
    When exporting from Subversion, Homebrew will use `HOMEBREW_SVN` if set,
    a Homebrew-built Subversion if installed, or the system-provided binary.

    Set this to force Homebrew to use a particular svn binary.

  * HOMEBREW\_TEMP:
    If set, instructs Homebrew to use `HOMEBREW_TEMP` as the temporary folder
    for building packages. This may be needed if your system temp folder and
    Homebrew Prefix are on different volumes, as OS X has trouble moving
    symlinks across volumes when the target does not yet exist.

    This issue typically occurs when using FileVault or custom SSD
    configurations.

  * HOMEBREW\_USE\_GCC:
    If set, instructs Homebrew to use gcc, even if the system default
    is currently set to LLVM.

  * HOMEBREW\_USE\_LLVM:
    If set, instructs Homebrew to use the LLVM front-ends to the GCC
    compilers.

    *NOTE*: Not all formulae build correctly with LLVM.

  * HOMEBREW\_VERBOSE:
    If set, instructs Homebrew to always assume `--verbose` when running
    commands.

## USING HOMEBREW BEHIND A PROXY

Homebrew uses several commands for downloading files (e.g. curl, git, svn).
Many of these tools can download via a proxy. It's common for these tools
to read proxy parameters from environment variables.

For the majority of cases setting `http_proxy` is enough. You can set this in
your shell profile, or you can use it before a brew command:

    http_proxy=http://<host>:<port> brew install foo

If your proxy requires authentication:

    http_proxy=http://<user>:<password>@<host>:<port> brew install foo

## SEE ALSO

Homebrew Wiki: <http://wiki.github.com/mxcl/homebrew/>

`git`(1), `git-log`(1)

## AUTHORS

Max Howell, a splendid chap.

## BUGS

See Issues on GitHub: <http://github.com/mxcl/homebrew/issues>


[ronn]: http://rtomayko.github.com/ronn/
        "Ronn"

[sinatra]: http://www.sinatrarb.com/
           "Sinatra"
