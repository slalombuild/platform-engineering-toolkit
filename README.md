<h1 align="center"><img src="docker.png" width="128" height="128" alt="Platform Engineering Toolkit"/><br/>Platform Engineering Toolkit</h1>

<!--[![License MIT](https://img.shields.io/badge/license-MIT-green)](./LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/slalombuild/platform-engineering-toolkit)](#users-and-community)-->

We are the **Slalom Build Platform Engineering** capability, and these are our container images with the tools we use for building, maintaining and securing infrastructure as code.

There are two different flavors, depending on your needs; **standard** and **full**. Standard contains most of the tools required for IaC projects, while Full contains additional languages and tools, such as Node, Go and Python.

Images are updated weekly (at least), and more frequently when tooling updates occur.

### Getting started

To use an image in your pipeline, pull from one of these URLs:

```bash
ghcr.io/slalombuild/pe-toolkit-standard-alpine:latest
ghcr.io/slalombuild/pe-toolkit-standard-ubuntu:latest
ghcr.io/slalombuild/pe-toolkit-full-alpine:latest
ghcr.io/slalombuild/pe-toolkit-full-ubuntu:latest
```
(All images are listed [here](https://github.com/orgs/SlalomBuild/packages?repo_name=platform-engineering-toolkit))

Or to use an image locally (assuming you already have docker setup), run:
```bash
docker pull ghcr.io/slalombuild/pe-toolkit-standard-ubuntu:latest
```

### FAQ

#### What tools do the Standard and Full images contain?

| Standard | Full |
| --- | --- |
| `terraform` | `terraform` |
| `atmos` | `atmos` |
| `curl` | `curl` |
| `bash` | `bash` |
| `jq` | `jq` |
| `yq` | `yq` |
| `figlet` | `figlet` |
| `unzip` | `unzip` |
| `zip` | `zip` |
| `git` | `git` |
| `shellcheck` | `shellcheck` |
| `nano` | `nano` |
| `tflint` | `tflint` |
| `tfsec` | `tfsec` |
| `opa` | `opa` |
| | `hadolint` |
| | `terraform-docs` |
| | `node` and `npm` |
| | `python` and `pip` |
| | `go` |

#### I'd like the image(s) to include x, can I add it?

Sure, go ahead and submit a PR. Some considerations when adding a tool -
- Should it be in Standard and/or Full?
- Tools should be added to all versions of the base OS. I.e. if it's added to `full-alpine`, it should also be added to `full-ubuntu`.
- If the tool significantly increases the image size, is it something we want in our toolkit, or something we'd run in a pipeline using an official image for the tool?
- Standard is intended to be lightweight, mainly used in pipelines, and Full is intended for development environments

#### I've made some changes and they don't work, how do I debug the problem?

1. Attempt to build the problematic image. Change to the relevant folder containing a `Dockerfile` under `images` and run 
   ```bash
   docker build -t test:latest .   
   ```
2. View the output for any errors.
3. If the container image builds successfully, start a shell in the container using 
   ```bash
   docker run --rm -it --entrypoint /bin/bash test
   ``` 
   and perform further debugging steps.

#### Which versions of binaries do we use?

We use the latest version of each tool at the time of building of the image.

#### Which base OS do we use?

We offer two options (currently); Alpine (latest) and Ubuntu (latest).

#### Which architectures do we support?

`amd64` and `arm64`. If there's an architecture you'd like an image for, please submit a PR.

### Contributions

If you'd like a tool added to the images, a different base OS, or a different architecture, please submit a PR. For bugs/security issues, please create a new issue and follow the instructions. Thanks.
