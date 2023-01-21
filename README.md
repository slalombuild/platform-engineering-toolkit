# platform-engineering-toolkit

We are the **Slalom Build Platform Engineering** capability, and these are our container images with the tools we use for building, maintaining and securing infrastructure as code. 

There are two different flavors, depending on your needs; **standard** and **full**. Standard contains most of the tools required for IaC projects, while Full contains additional languages and tools, such as Node, Go and Python.

Images are updated weekly (at least), and more frequently when tooling updates occur.

### Getting started

To use an image in your pipeline, pull from one of these URLs:

```bash
ghcr.io/SlalomBuild/pe-toolkit-standard-alpine-amd64:latest
ghcr.io/SlalomBuild/pe-toolkit-standard-ubuntu-amd64:latest
ghcr.io/SlalomBuild/pe-toolkit-full-alpine-amd64:latest
ghcr.io/SlalomBuild/pe-toolkit-full-ubuntu-amd64:latest
```
(All images are listed [here](https://github.com/orgs/SlalomBuild/packages?repo_name=platform-engineering-toolkit))

Or to use an image locally (assuming you already have docker setup), run:
```bash
docker pull ghcr.io/SlalomBuild/pe-toolkit-standard-ubuntu-amd64:latest
```

### FAQ

#### What tools do the Standard and Full images contain?

| Standard | Full |
| --- | --- |
| `terraform`<br/> `atmos`<br/> `curl`<br/> `bash`<br/> `jq`<br/> `yq`<br/> `figlet`<br/> `unzip`<br/> `zip`<br/> `git`<br/> `shellcheck`<br/> `nano`<br/> | _everything in standard_<br/> `aws-azure-login`<br/> `node` and `npm`<br/> `python` and `pip`<br/> `go`<br/> |

#### Which versions do we use?

We use the latest version of each tool at the time of building of the image.

#### Which base OS do we use?

We offer two options (currently); Alpine (latest) and Ubuntu (latest).

#### Which architectures do we support?

`amd64`. If there's an architecture you'd like an image for, please submit a PR.

### Contributions

If you'd like a tool added to the images, a different base OS, or a different architecture, please submit a PR. For bugs/security issues, please create a new issue and follow the instructions. Thanks.

### License

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
