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
  nano && \
  rm -rf /var/cache/apk/*

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