FROM mcr.microsoft.com/powershell:ubuntu-focal

LABEL maintainer="alex.bocharov@outlook.com"

ARG GITHUB_RUNNER_VERSION

ENV \
    RUNNER_NAME="" \
    RUNNER_WORK_DIRECTORY="_work" \
    RUNNER_TOKEN="" \
    RUNNER_REPOSITORY_URL="" \
    RUNNER_LABELS="" \
    RUNNER_ALLOW_RUNASROOT=true \
    GITHUB_ACCESS_TOKEN="" \
    RUNNER_INSTALL_FOLDER=/opt/github/actions-runner

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
        git \
        wget \
        jq \
    # Download the Linux package and save it
    && apt-get dist-upgrade -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p ${RUNNER_INSTALL_FOLDER} \
    && chmod -R 755 ${RUNNER_INSTALL_FOLDER}

WORKDIR ${RUNNER_INSTALL_FOLDER}

RUN GITHUB_RUNNER_VERSION=${GITHUB_RUNNER_VERSION:-$(curl --silent "https://api.github.com/repos/actions/runner/releases/latest" | grep tag_name | sed -E 's/.*"v([^"]+)".*/\1/')} \
    && curl -L -O https://github.com/actions/runner/releases/download/v${GITHUB_RUNNER_VERSION}/actions-runner-linux-x64-${GITHUB_RUNNER_VERSION}.tar.gz \
    && tar -zxf actions-runner-linux-x64-${GITHUB_RUNNER_VERSION}.tar.gz \
    && rm -f actions-runner-linux-x64-${GITHUB_RUNNER_VERSION}.tar.gz \
    && ./bin/installdependencies.sh \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# Set entrypoint.
COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["./bin/runsvc.sh"]