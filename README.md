<h1 align="center"><img src="docker.png" width="128" height="128" alt="Platform Engineering Toolkit"/><br/>Platform Engineering Toolkit</h1>

<!--[![License MIT](https://img.shields.io/badge/license-MIT-green)](./LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/slalombuild/platform-engineering-toolkit)](#users-and-community)-->

We are the **Slalom Build Platform Engineering** capability, and these are our container images with the tools we use for building, maintaining and securing infrastructure as code.

There are two different flavors, depending on your needs; **standard** and **full**. Standard contains most of the tools required for IaC projects, while Full contains additional languages and tools, such as Node, Go and Python.

Images are updated weekly (at least), and more frequently when tooling updates occur.

### Getting started

To use an image in your pipeline, pull from one of these URLs:

```bash
ghcr.io/slalombuild/pe-toolkit-standard-alpine-amd64:latest
ghcr.io/slalombuild/pe-toolkit-standard-ubuntu-amd64:latest
ghcr.io/slalombuild/pe-toolkit-full-alpine-amd64:latest
ghcr.io/slalombuild/pe-toolkit-full-ubuntu-amd64:latest
```
(All images are listed [here](https://github.com/orgs/SlalomBuild/packages?repo_name=platform-engineering-toolkit))

Or to use an image locally (assuming you already have docker setup), run:
```bash
docker pull ghcr.io/slalombuild/pe-toolkit-standard-ubuntu-amd64:latest
```

### FAQ

#### What tools do the Standard and Full images contain?

| Standard | Full |
| --- | --- |
| `terraform`<br/> `atmos`<br/> `curl`<br/> `bash`<br/> `jq`<br/> `yq`<br/> `figlet`<br/> `unzip`<br/> `zip`<br/> `git`<br/> `shellcheck`<br/> `nano`<br/> | _everything in standard_<br/> `terraform-docs`<br/> `node` and `npm`<br/> `python` and `pip`<br/> `go`<br/> |

#### I'd like the image(s) to include x, can I add it?

Sure, go ahead and submit a PR. Some considerations when adding a tool -
- Should it be in Standard and/or Full?
- Tools should be added to all versions of the base OS. I.e. if it's added to `full-alpine-amd64`, it should also be added to `full-ubuntu-amd64`.
- If the tool significantly increases the image size, is it something we want in our toolkit, or something we'd run in a pipeline using an official image for the tool?
- Standard is intended to be lightweight, mainly used in pipelines, and Full is intended for development environments

#### Which versions do we use?

We use the latest version of each tool at the time of building of the image.

#### Which base OS do we use?

We offer two options (currently); Alpine (latest) and Ubuntu (latest).

#### Which architectures do we support?

`amd64`. If there's an architecture you'd like an image for, please submit a PR.

### Contributions

If you'd like a tool added to the images, a different base OS, or a different architecture, please submit a PR. For bugs/security issues, please create a new issue and follow the instructions. Thanks.
