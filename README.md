lgdock is a tool for preparing LaTeX papers. It only depends on having Docker installed on a host, and also works with boot2docker.

## Usage

To start, you can clone this repository or otherwise drop build.gradle into your paper's directory.
You will need to have Gradle and Docker installed. Your Docker installation will need to expose
its HTTP interface. If you are using boot2docker on a Windows or Mac computer, this is the
default configuration. If you are on a Linux host with Docker directly installed, check out
[this blog post](http://www.virtuallyghetto.com/2014/07/quick-tip-how-to-enable-docker-remote-api.html).

Once you have tools installed, you need to tell gradle where to find Docker and your LaTex file. The
script uses Gradle properties for this. You can use the provided gradle.properties file OR just set
properties at the command-line like so:
```
gradle -PdockerUrl="https://..." ...
```
With these properties set, you can now run tasks. A simple build of a PDF currently requires running two
tasks. (Hopefully, these can be safely linked in the future!)

```
gradle buildImage
gradle buildPaper
```

This will produce "example.pdf" in your current directory.

## Available Tasks

Available tasks are:
* buildImage - build the base Docker image
* buildPaper - Run the sequence of pdflatex, bibtex, pdflatex, pdflatex to generate a PDF with optional
bibliography
* cleanAll - remove paper files and the Docker image. NOT recommended unless you are tweaking the image
* cleanPaper - remove intermediate paper files

## Under the Covers

The Dockerfile is defined inline in the build.gradle script. It installs a basic set of texlive packages
and R statistics packages. The Gradle tasks run some commands locally and some within Docker containers.

## Why Bro?

It may seem like Gradle and Docker are much heavier dependencies than the likes of LaTeX and R. First,
I'm not 100% sure that's the truth, because LaTeX distributions tend to be HUGE. However, I still like
the portability of having a known LaTeX and R setup that goes with me. Also, Boot2Docker is very easy
to install, and affords users the ability to use these tools in their more natural *nix environment
without having to remember all of the quirks by hand.

## What's next?

I would like to add additional tasks to this tool for building tables, figures, and R outputs for LaTex
documents. I don't know when I'll have time to do this as I'm currently working full-time on top of
working on dissertation research; but feel free to post an issue if you have ideas, or even better, to
submit PRs so we can REALLY get this rolling.

Thanks for stopping by!


