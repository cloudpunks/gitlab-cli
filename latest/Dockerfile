FROM ghcr.io/cloudpunks/alpine:3.24@sha256:d1f1c104aabb0279a75d2e8feb74a1f01fd75ae1ac7337a1a113ae5d8ddb289f
ENTRYPOINT [""]

# renovate: datasource=gitlab-releases depName=gitlab-org/cli
ENV GITLAB_CLI_VERSION=1.118.0

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
