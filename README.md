# Dist::Zilla Bash Completion

Basic tab completion for [dzil](http://dzil.org/), the Perl distribution power-tool for CPAN distribution.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# Introduction

The completion implementation requires `dzil` to be installed (of course), it uses `dzil` built-in `commands` command to extract what is available and makes this accessible for tab completion.

In addition installed Dist::Zilla command plugins are automatically exposed by `dzil` meaning that tab completions are also automatically supported.

This is based on Dist::Zilla 6.009.

## Usage

```bash
$ dzil <tab>
add    build    commands   help    listdeps   nop   run   smoke   authordeps   clean  install  new        release setup      test
```

If you have additional Dist::Zilla::App::Command plugins installed this will be discovered by Dist::Zilla and hence listed by this utility automatically.

Example: [Dist::Zilla::App::Command::cover](https://metacpan.org/pod/Dist::Zilla::App::Command::cover)

```bash
$ dzil <tab>
add    build    commands   help    listdeps   nop   run   smoke   authordeps   clean  install  new        release setup      cover test
```

`listdeps` offer the additional completions:

```bash
$ dzil listdeps <tab>
--missing --develop --author --missing --requires --no-requires --recommends --no-recommends --suggests --no-suggests --versions --cpanm-versions --json --omit-cores
```

`authordeps` offer the additional completions:

```bash
$ dzil authordeps <tab>
--root --missing --versions
```

## Download

```bash
$ curl https://raw.githubusercontent.com/jonasbn/bash_completion_dzil/master/dzil > dzil
```

## Installation

When downloaded you have to install the completion implementation. Where your completions are located might vary.

### Personal

If you want to install them for your personal use, do the following.

Create the file: `~/.bash_completion`, containing the code below:

```bash
for bcfile in ~/.bash_completion.d/* ; do
  . $bcfile
done
```

Ref: [ServerFault.com: _Standard place for user defined bash_completion.d scripts?_](https://serverfault.com/questions/506612/standard-place-for-user-defined-bash-completion-d-scripts)

Create a directory for your completions:

```bash
$ mkdir ~/.bash_completion.d
```

Copy your completions into the newly created directory:

```bash
$ cp dzil ~/.bash_completion.d/
```

Start a new shell and you should be good to go.

### System-wide example from Debian

Based on [an introduction](https://debian-administration.org/article/316/An_introduction_to_bash_completion_part_1) to `bash` completions on Debian.

```bash
$ sudo cp dzil /etc/bash_completion.d/
```

### System-wide example from OSX

This assumes you are using **Homebrew**

Do note that paths vary based on whether you are using `bash` 3 or 4

#### `bash` 3 (Formula: `bash-completions`):

```bash
$ cp dzil /usr/local/etc/bash_completion.d/
```

And to activate right away:

```bash
$ source  /usr/local/etc/bash_completion.d/dzil
```

#### `bash` 4 (Formula: `bash-completions2`)

```bash
$ cp dzil /usr/local/share/bash-completion/completions/
```

And to activate right away:

```bash
$ source /usr/local/share/bash-completion/completions/dzil
```

## Motivation

`dzil` is an important tool in my toolchain, so I wanted to have easy access to all the options available.

## History

- 1.0.0
    + Initial version working with `bash` version 4.

## See Also

A more elaborate piece of documentation on `bash` completions is available from **The Linux Documentation Project** in the [Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html/tabexpansion.html).

From the [GNU Documentation](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion.html).

Good two-part article, "An Introduction to Bash Completion": [Part 1](https://debian-administration.org/article/316/An_introduction_to_bash_completion_part_1) and [Part 2](https://debian-administration.org/article/317/An_introduction_to_bash_completion_part_2).

Please note that this experimental implementation has only been tested with `bash` version 3 (see version 1.0.0).

Versions after version 1.0.0 have been tested with `bash` version 4.

The most comprehensive collection of `bash` completions I have come across is [the one](https://github.com/scop/bash-completion) from the **Debian Linux distribution**. It is also the one offered for OSX via **Homebrew**.

## License

This is made available under the MIT license, see separate license file.

## Copyright

:copyright: jonasbn 2017
