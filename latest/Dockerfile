FROM ghcr.io/cloudpunks/alpine:3.24@sha256:c05a9a0ce1b3d9e2f216b0024f499a562977cfa67174c20e9f9a19dee301ad04
ENTRYPOINT [""]

# renovate: datasource=gitlab-releases depName=gitlab-org/cli
ENV GITLAB_CLI_VERSION=1.113.0

ARG TARGETARCH

RUN apk update && \
  apk upgrade && \
  mkdir /tmp/cli && \
  cd /tmp/cli && \
  case "${TARGETARCH}" in \
    'amd64') \
      curl -sSLo- https://gitlab.com/gitlab-org/cli/-/releases/v${GITLAB_CLI_VERSION}/downloads/glab_${GITLAB_CLI_VERSION}_linux_amd64.tar.gz | tar xvzf -; \
      ;; \
    'arm64') \
      curl -sSLo- https://gitlab.com/gitlab-org/cli/-/releases/v${GITLAB_CLI_VERSION}/downloads/glab_${GITLAB_CLI_VERSION}_linux_arm64.tar.gz | tar xvzf -; \
      ;; \
    *) echo >&2 "error: unsupported architecture '${TARGETARCH}'"; exit 1 ;; \
  esac && \
  mv /tmp/cli/bin/glab /usr/local/bin/glab && \
  rm -rf /tmp/cli && \
  rm -rf /var/cache/apk/*
