FROM python:3.13-bookworm

ARG USERNAME=vscode
ARG GROUPNAME=vscode
ARG UID
ARG GID
ARG WORKDIR=/app

RUN groupadd -g ${GID} ${GROUPNAME} && \
    useradd -m -s /bin/bash -u ${UID} -g ${GID} ${USERNAME}

RUN apt-get update && \
    apt-get install -y bash-completion

RUN mkdir ${WORKDIR} && chown ${USERNAME}:${GROUPNAME} ${WORKDIR}

USER ${USERNAME}
WORKDIR ${WORKDIR}
COPY requirements.txt requirements-dev.txt ./
RUN python3 -m venv .venv && \
    . .venv/bin/activate && \
    pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements-dev.txt
