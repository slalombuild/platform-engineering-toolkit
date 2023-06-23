FROM alpine:latest

RUN apk update && \
  apk upgrade && \
  apk add --update --no-cache \
  curl \
  bash \
  jq \
  yq \
  figlet \
  unzip \
  zip \
  git \
  shellcheck \
  nano \
  tar && \
  rm -rf /var/cache/apk/*

# Install languages, libraries and frameworks
RUN apk add --update \
  nodejs \
  npm \
  python3 \
  py3-pip && \
  rm -rf /var/cache/apk/*

# Install golang
COPY --from=golang:alpine3.17 /usr/local/go/ /usr/local/go/
ENV PATH="/usr/local/go/bin:${PATH}"

# Install terraform (https://github.com/hashicorp/terraform)
RUN export tfrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/hashicorp/terraform/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing terraform v${tfrelease}" \
  && wget https://releases.hashicorp.com/terraform/${tfrelease}/terraform_${tfrelease}_linux_amd64.zip \
  && unzip terraform_${tfrelease}_linux_amd64.zip \
  && chmod +x terraform \
  && mv terraform /usr/local/bin/terraform \
  && rm terraform_${tfrelease}_linux_amd64.zip

# Install atmos (https://github.com/cloudposse/atmos)
RUN export atmosrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/cloudposse/atmos/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing atmos v${atmosrelease}" \
  && wget https://github.com/cloudposse/atmos/releases/download/v${atmosrelease}/atmos_${atmosrelease}_linux_amd64 \
  && chmod +x atmos_${atmosrelease}_linux_amd64 \
  && mv atmos_${atmosrelease}_linux_amd64 /usr/local/bin/atmos

# Install terraform-docs
RUN export tfdocsrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/terraform-docs/terraform-docs/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing terraform-docs v${tfdocsrelease}" \
  && wget https://github.com/terraform-docs/terraform-docs/releases/download/v${tfdocsrelease}/terraform-docs-v${tfdocsrelease}-linux-amd64.tar.gz \
  && tar -xzf terraform-docs-v${tfdocsrelease}-linux-amd64.tar.gz -C /usr/local/bin terraform-docs \
  && chmod +x /usr/local/bin/terraform-docs \
  && rm terraform-docs-v${tfdocsrelease}-linux-amd64.tar.gz

# Install Packer https://github.com/hashicorp/packer()
ARG packer_version=1.8.5
ARG packer_zip_url=https://releases.hashicorp.com/packer/${packer_version}/packer_${packer_version}_linux_amd64.zip
RUN wget -nv ${packer_zip_url} \
  && unzip -d /usr/local/bin packer_${packer_version}_linux_amd64.zip \
  && rm packer_${packer_version}_linux_amd64.zip

# Install hadolint (https://github.com/hadolint/hadolint)
ARG hadolint_version=2.12.0
RUN wget -nv https://github.com/hadolint/hadolint/releases/download/v${hadolint_version}/hadolint-Linux-x86_64 \
  && mv hadolint-Linux-x86_64 /usr/local/bin/hadolint \
  && chmod +x /usr/local/bin/hadolint

# Install tflint (https://github.com/terraform-linters/tflint)
RUN export tflintrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/terraform-linters/tflint/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing tflint v${tflintrelease}" \
  && wget https://github.com/terraform-linters/tflint/releases/download/v${tflintrelease}/tflint_linux_amd64.zip \
  && unzip -d /usr/local/bin tflint_linux_amd64.zip \
  && chmod +x /usr/local/bin/tflint \
  && rm tflint_linux_amd64.zip

# Install tfsec (https://github.com/aquasecurity/tfsec)
RUN export tfsecrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/aquasecurity/tfsec/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing tfsec v${tfsecrelease}" \
  && wget https://github.com/aquasecurity/tfsec/releases/download/v${tfsecrelease}/tfsec-linux-amd64 \
  && chmod +x tfsec-linux-amd64 \
  && mv tfsec-linux-amd64 /usr/local/bin/tfsec

# Install Open Policy Agent (https://openpolicyagent.org)
RUN curl -L -o opa https://openpolicyagent.org/downloads/latest/opa_linux_amd64 \
  && chmod +x opa \
  && mv opa /usr/local/bin/opa
