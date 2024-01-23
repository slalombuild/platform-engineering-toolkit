FROM alpine:latest

ARG TARGETPLATFORM

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
  && case ${TARGETPLATFORM} in \
  "linux/arm64")  ARCHITECTURE=arm64  ;; \
  *)              ARCHITECTURE=amd64   ;; \
  esac && \
  && echo "Installing terraform v${tfrelease} (${ARCHITECTURE})" \
  && wget https://releases.hashicorp.com/terraform/${tfrelease}/terraform_${tfrelease}_linux_${ARCHITECTURE}.zip \
  && unzip terraform_${tfrelease}_linux_${ARCHITECTURE}.zip \
  && chmod +x terraform \
  && mv terraform /usr/local/bin/terraform \
  && rm terraform_${tfrelease}_linux_${ARCHITECTURE}.zip

# Install atmos (https://github.com/cloudposse/atmos)
RUN export atmosrelease="$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/cloudposse/atmos/releases/latest | awk -F / '{print substr($NF,2);}')" \
  && case ${TARGETPLATFORM} in \
  "linux/arm64")  ARCHITECTURE=arm64  ;; \
  *)              ARCHITECTURE=amd64   ;; \
  esac && \
  && echo "Installing atmos v${atmosrelease} (${ARCHITECTURE})" \
  && wget https://github.com/cloudposse/atmos/releases/download/v${atmosrelease}/atmos_${atmosrelease}_linux_${ARCHITECTURE} \
  && chmod +x atmos_${atmosrelease}_linux_${ARCHITECTURE} \
  && mv atmos_${atmosrelease}_linux_${ARCHITECTURE} /usr/local/bin/atmos

# Install tflint (https://github.com/terraform-linters/tflint)
RUN export tflintrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/terraform-linters/tflint/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && case ${TARGETPLATFORM} in \
  "linux/arm64")  ARCHITECTURE=arm64  ;; \
  *)              ARCHITECTURE=amd64   ;; \
  esac && \
  && echo "Installing tflint v${tflintrelease} (${ARCHITECTURE})" \
  && wget https://github.com/terraform-linters/tflint/releases/download/v${tflintrelease}/tflint_linux_${ARCHITECTURE}.zip \
  && unzip -d /usr/local/bin tflint_linux_${ARCHITECTURE}.zip \
  && chmod +x /usr/local/bin/tflint \
  && rm tflint_linux_${ARCHITECTURE}.zip

# Install tfsec (https://github.com/aquasecurity/tfsec)
RUN export tfsecrelease="$(curl -Ls -o /dev/null -w %{url_effective} "https://github.com/aquasecurity/tfsec/releases/latest" | awk -F / '{print substr($NF,2);}')" \
  && case ${TARGETPLATFORM} in \
  "linux/arm64")  ARCHITECTURE=arm64  ;; \
  *)              ARCHITECTURE=amd64   ;; \
  esac && \
  && echo "Installing tfsec v${tfsecrelease} (${ARCHITECTURE})" \
  && wget https://github.com/aquasecurity/tfsec/releases/download/v${tfsecrelease}/tfsec-linux-${ARCHITECTURE} \
  && chmod +x tfsec-linux-${ARCHITECTURE} \
  && mv tfsec-linux-${ARCHITECTURE} /usr/local/bin/tfsec

# Install Open Policy Agent (https://openpolicyagent.org)
RUN case ${TARGETPLATFORM} in \
  "linux/arm64")  ARCHITECTURE=arm64  ;; \
  *)              ARCHITECTURE=amd64   ;; \
  esac && \
  && echo "Installing opa (${ARCHITECTURE})" \
  curl -L -o opa https://openpolicyagent.org/downloads/latest/opa_linux_${ARCHITECTURE}_static \
  && chmod +x opa \
  && mv opa /usr/local/bin/opa