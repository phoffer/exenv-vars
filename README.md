# exenv-vars

This is a plugin for [exenv](https://github.com/mururu/exenv)
that lets you set global and project-specific environment variables
before spawning Ruby processes.

This is a port of the rbenv-vars plugin for rbenv.

## Installation

Make sure you have the latest version of exenv, then run:

    git clone https://github.com/phoffer/exenv-vars.git $(exenv root)/plugins/exenv-vars

## Usage

Define environment variables in an `.exenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    MAGIC_API_KEY=14aebc729

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `GEM_PATH`:

    GEM_PATH=$GEM_PATH:/u/shared/gems

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

    JAVA_OPTS?=-server -Xmx768m -Xms768m -Xmn128m -Xss20m

In the above case, `JAVA_OPTS` will only be set if `$JAVA_OPTS` is
currently empty (i.e., if `[ -z "$JAVA_OPTS" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.exenv/vars` file will be set
first. Then variables specified in `.exenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.exenv-vars` file in the current directory are set last.

Use the `exenv vars` command to print all environment variables in the
order they'll be set.

## Version History

**1.0.0** (February 19, 2019)

* Port from rbenv-vars and initial release

## License

&copy; 2019 Paul Hoffer. Released under the MIT license. See
`LICENSE` for details.

Special thanks to Sam Stephenson for creating the original rbenv-vars
