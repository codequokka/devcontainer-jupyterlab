FROM python:3.13-bookworm

ARG USERNAME=vscode
ARG GROUPNAME=vscode
ARG UID
ARG GID
ARG WORKDIR=/app

RUN apt-get update && \
    apt-get install -y bash-completion nodejs sudo

RUN groupadd -g ${GID} ${GROUPNAME} && \
    useradd -m -s /bin/bash -u ${UID} -g ${GID} -G sudo ${USERNAME} && \
    echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN mkdir ${WORKDIR} && chown ${USERNAME}:${GROUPNAME} ${WORKDIR}

USER ${USERNAME}
WORKDIR ${WORKDIR}
COPY requirements.txt requirements-dev.txt ./
COPY jupyter_lab_config.py ./
RUN python3 -m venv .venv && \
    . .venv/bin/activate && \
    pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements-dev.txt
