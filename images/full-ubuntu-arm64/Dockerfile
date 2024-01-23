FROM ubuntu:latest

RUN apt update -yq && \
  apt upgrade -yq && \
  apt install -yq --no-install-recommends --no-install-suggests \
  ca-certificates \
  apt-transport-https \
  wget \
  curl \
  bash \
  jq \
  figlet \
  unzip \
  zip \
  git \
  shellcheck \
  nano \
  tar

# Install languages, libraries and frameworks
RUN apt install -yq --no-install-recommends --no-install-suggests \
  nodejs \
  npm \
  python3 \
  python3-pip \
  golang && \
  rm -rf /var/lib/apt/lists/*

# Install terraform (https://github.com/hashicorp/terraform)
RUN export tfrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/hashicorp/terraform/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing terraform v${tfrelease}" \
  && wget https://releases.hashicorp.com/terraform/${tfrelease}/terraform_${tfrelease}_linux_arm64.zip \
  && unzip terraform_${tfrelease}_linux_arm64.zip \
  && chmod +x terraform \
  && mv terraform /usr/local/bin/terraform \
  && rm terraform_${tfrelease}_linux_arm64.zip

# Install atmos (https://github.com/cloudposse/atmos)
RUN export atmosrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/cloudposse/atmos/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing atmos v${atmosrelease}" \
  && wget https://github.com/cloudposse/atmos/releases/download/v${atmosrelease}/atmos_${atmosrelease}_linux_arm64 \
  && chmod +x atmos_${atmosrelease}_linux_arm64 \
  && mv atmos_${atmosrelease}_linux_arm64 /usr/local/bin/atmos

# Install terraform-docs
RUN export tfdocsrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/terraform-docs/terraform-docs/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing terraform-docs v${tfdocsrelease}" \
  && wget https://github.com/terraform-docs/terraform-docs/releases/download/v${tfdocsrelease}/terraform-docs-v${tfdocsrelease}-linux-arm64.tar.gz \
  && tar -xzf terraform-docs-v${tfdocsrelease}-linux-arm64.tar.gz -C /usr/local/bin terraform-docs \
  && chmod +x /usr/local/bin/terraform-docs \
  && rm terraform-docs-v${tfdocsrelease}-linux-arm64.tar.gz

# Install Packer https://github.com/hashicorp/packer()
ARG packer_version=1.8.5
ARG packer_zip_url=https://releases.hashicorp.com/packer/${packer_version}/packer_${packer_version}_linux_arm64.zip
RUN wget -nv ${packer_zip_url} \
  && unzip -d /usr/local/bin packer_${packer_version}_linux_arm64.zip \
  && rm packer_${packer_version}_linux_arm64.zip

# Install hadolint (https://github.com/hadolint/hadolint)
ARG hadolint_version=2.12.0
RUN wget -nv https://github.com/hadolint/hadolint/releases/download/v${hadolint_version}/hadolint-Linux-x86_64 \
  && mv hadolint-Linux-x86_64 /usr/local/bin/hadolint \
  && chmod +x /usr/local/bin/hadolint

# Install tflint (https://github.com/terraform-linters/tflint)
RUN export tflintrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/terraform-linters/tflint/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing tflint v${tflintrelease}" \
  && wget https://github.com/terraform-linters/tflint/releases/download/v${tflintrelease}/tflint_linux_arm64.zip \
  && unzip -d /usr/local/bin tflint_linux_arm64.zip \
  && chmod +x /usr/local/bin/tflint \
  && rm tflint_linux_arm64.zip

# Install tfsec (https://github.com/aquasecurity/tfsec)
RUN export tfsecrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/aquasecurity/tfsec/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing tfsec v${tfsecrelease}" \
  && wget https://github.com/aquasecurity/tfsec/releases/download/v${tfsecrelease}/tfsec-linux-arm64 \
  && chmod +x tfsec-linux-arm64 \
  && mv tfsec-linux-arm64 /usr/local/bin/tfsec

# Install Open Policy Agent (https://openpolicyagent.org)
RUN curl -L -o opa https://openpolicyagent.org/downloads/latest/opa_linux_arm64_static \
  && chmod +x opa \
  && mv opa /usr/local/bin/opa
