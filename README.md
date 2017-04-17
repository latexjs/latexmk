# latexmk for Latexjs (mirror)

To be a complete LaTeX toolchain we need something like `latexmk` to be able to perform the correct number of executions of `pdflatex` and `bibtex`, and unfortunately there isn't a good native (and hence Emscripten-able) or Javascript solution for this. As a stopgap, we currently use `latexmk` and rely on a system Perl interpreter for macOS/Linux (a reasonably safe bet) and use [`pp`](http://search.cpan.org/~autrijus/PAR/script/pp) to compile a standalone Windows binary of `latexmk` for Windows (where we can't guarantee at all that a perl interpreter will be kicking around).

This repository stores the current version of `latexmk` that we use in `Latexjs` and the compiled Windows binary version.

## Bumping to a new version of latexmk

On Windows:

1. Install [Strawberry Perl](http://strawberryperl.com/)
2. Following [these instructions](http://www.cpan.org/modules/INSTALL.html) first install the cpanm tool:
```
cpan App::cpanminus
```
3. Then use this to install `pp`:
```
cpanm pp
```

With this done, we can now build a binary of latexmk:

1. Download the latest version of [latexmk](www.phys.psu.edu/~collins/software/latexmk-jcc/)
2. Run
```
pp -M FindBin -o latexmk.exe latexmk.pl
```
To build a Windows binary. Note that we manually include `FindBin` as we use this in our custom latexmk config perl script.

3. Commit and push the changes
4. Rebuild [`latexjs/latexjs`](https://github.com/latexjs/latexjs/blob/master/latexjs/Dockerfile) to include the new version in an update of `Latexjs`.
