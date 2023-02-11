# Bali Unit Testing Framework

Bali Unit Testing Framework is a framework for testing code written using VoltScript, the evolution of LotusScript delivered as part of HCL Volt MX Go. The framework can also be used for LotusScript, with modifications (see below on new language functions used). There are deliberately no dependencies on any LSXs (e.g nlsxbe.dll). None should be added, it will make it dependent on a particular implementation. Create separate classes derived from BaliCustomTester to test individual LSXs or custom classes.

This fork is adapted to compile with LotusScript in Notes/Domino 12.0.x.

## Downloading

To download the code, go to [Releases](/releases). The script is in BaliTestRUnner.bss, in the Assets for each release. This can be copied into a Script Library in your NSF. This corresponds to [src/BaliTestRunner.bss](/src/BaliTestRunner.bss) at the time of the specific release.

## Writing BaliUnit Tests

See [Writing Units Tests](/docs/Writing-Unit-Tests/index.md).

## Core Functions Used

Obviously the code runs certain core language functions. These are documented in [Core Functions](/docs/CoreFunctions.md).

There are three new VoltScript language functions used - Try/Catch/Finally and GetThreadInfo(12) in BaliTestRunner.bss and ++/-- in SampleBeforeAfterTester.bss.

### Documentation

Documentation uses [Material for MKDocs](https://squidfunk.github.io/mkdocs-material/getting-started/#installation), which uses Markdown files in the docs directory. The [awesome-pages](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin) is the only additional plugin in use.

This can be previewed using a Docker container or locally. To run locally, follow the [Material for MKDocs documentation](https://squidfunk.github.io/mkdocs-material/getting-started/#with-pip) and the steps to install awesome-pages plugin on their GitHub.

To use with Docker, a Dockerfile has been included. In a terminal, navigate to the docker directory. Issue the command `docker build -t mkdocs-plus .` This creates a Docker image based on MKDocs Material image, adding the additional plugin. If you are using a M1 Mac, a different starting image will be needed, `ghcr.io/afritzler/mkdocs-material`, see https://github.com/afritzler/mkdocs-material.

Once the Docker container is created, it can be started as a temporary container by:

1. Open a terminal and navigate to this directory.
2. Issue the command `docker run --rm -it -p 8000:8000 -v ${PWD}:/docs mkdocs-plus`. On Windows, `${PWD}` maps to the current directory for PowerShell, `%cd%` for a normal Windows cmd prompt. Other MKDocs commands can be appended, as required - see MKDocs documentation for more details.
