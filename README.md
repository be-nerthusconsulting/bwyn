# Build What You Need (BWYN)
`bwyn` is a tool aimed at multi-modules _Maven_ projects with very long build times.

Often we lose time building them entirely even if we just modified some classes. `bwyn` relies on _Git_ to determine what modules have been impacted by our changes and only them (and the modules that depend upon them).

How does it work? You simply use `bwyn` instead of `mvn` to build your project:
```shell
bwyn clean install
```
The first time it runs, `bwyn` will build the entire project, as would `mvn`. It'll then store the _Git_ references that was built in `.bwyn/lastBuild`.

After that, it'll use that reference to determine impacted modules and build only them so that `bwyn clean install` translates into `mvn clean install --projects module-a,module-b --also-make-dependents` (or `mvn clean install --pl module-a,module-b -amd` if using abbreviated options).

It's also possible to provide `--from=<git_ref>` and `--to=<git_ref>` options which allows you to control where `bwyn` is looking for changes. `--to` reference will then be saved in `.bwyn/lastBuild`.

## Installation
To install `bwyn`, follow these instructions:
1. Download [the bwyn bash script][bwyn-script-link] (or copy the content to a local file)
2. Add the directory containing the file to your `PATH`
3. Open a terminal (Linux/Unix only, for Windows see WSL, MinGW or Cygwin) and `cd` into your project workspace
4. Run `bwyn` as you would `mvn` (it only works for multi-modules project for now)

[bwyn-script-link]: src/main/scripts/bwyn
