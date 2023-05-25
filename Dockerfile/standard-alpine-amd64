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
  && wget https://releases.hashicorp.com/terraform/${tfrelease}/terraform_${tfrelease}_linux_amd64.zip \
  && unzip terraform_${tfrelease}_linux_amd64.zip \
  && mv terraform /usr/bin/terraform \
  && rm terraform_${tfrelease}_linux_amd64.zip

# Install atmos (https://github.com/cloudposse/atmos)
RUN export atmosrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/cloudposse/atmos/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing atmos v${atmosrelease}" \
  && wget https://github.com/cloudposse/atmos/releases/download/v${atmosrelease}/atmos_${atmosrelease}_linux_amd64 \
  && mv atmos_${atmosrelease}_linux_amd64 /usr/bin/atmos \
  && chmod +x /usr/bin/atmos

# Install tflint (https://github.com/terraform-linters/tflint)
RUN export tflintrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/terraform-linters/tflint/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing tflint v${tflintrelease}" \
  && wget https://github.com/terraform-linters/tflint/releases/download/v${tflintrelease}/tflint_linux_amd64.zip \
  && unzip tflint_linux_amd64.zip \
  && mv tflint /usr/bin/tflint \
  && chmod +x /usr/bin/tflint

# Install tfsec (https://github.com/aquasecurity/tfsec)
RUN export tfsecrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/aquasecurity/tfsec/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && echo "Installing tfsec v${tfsecrelease}" \
  && wget https://github.com/aquasecurity/tfsec/releases/download/v${tfsecrelease}/tfsec-linux-amd64 \
  && mv tfsec-linux-amd64 /usr/bin/tfsec \
  && chmod +x /usr/bin/tfsec
