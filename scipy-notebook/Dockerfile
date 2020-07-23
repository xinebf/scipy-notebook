# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/scipy-notebook:latest

LABEL maintainer="xinebf <zhxz@cadavez.xyz>"

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    octave gnuplot fonts-freefont-otf vim && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN conda install --quiet --yes \
    'jupyterlab-git' \
    'octave_kernel' \
    && \
    conda clean --all -f -y && \
    jupyter labextension install @jupyterlab/git --no-build && \
    jupyter lab build -y && \
    jupyter lab clean -y && \
    npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

