# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=jupyter/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="xinebf <zhxz@cadavez.xyz>"

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends octave gnuplot vim && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN pip install --quiet --no-cache-dir \
    'jupyterlab-git' \
    'octave_kernel' \
    'jupyter-lsp' \
    'python-language-server[all]' \
    && \
    jupyter labextension install @jupyterlab/git --no-build && \
    jupyter labextension install @krassowski/jupyterlab_go_to_definition --no-build && \
    jupyter labextension install @krassowski/jupyterlab-lsp --no-build && \
    jupyter lab build -y && \
    jupyter lab clean -y && \
    npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

