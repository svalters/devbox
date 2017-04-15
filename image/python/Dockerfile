# vim: set foldmarker=[[,]] foldlevel=0 foldmethod=marker spell:
# ------------------------------------------------------------------------------
# -> Base image [[
# ------------------------------------------------------------------------------

FROM python:latest

# ]]
# ------------------------------------------------------------------------------
# -> Install base packages [[
# ------------------------------------------------------------------------------

RUN apt-get update && apt-get install -y \
    git \
    mercurial \
    wget \
    curl \
    ssmtp

# ]]
# ------------------------------------------------------------------------------
# -> SQLite [[
# ------------------------------------------------------------------------------

ARG INSTALL_SQLITE=false

RUN if [ ${INSTALL_SQLITE} = true ]; then \
    apt-get update && apt-get install -y \
        sqlite \
;fi

# ]]
# ------------------------------------------------------------------------------
# -> Install Python packages [[
# ------------------------------------------------------------------------------

RUN pip install \
    uwsgi \
    virtualenv \
    virtualenvwrapper \
    autoenv

# ]]
# ------------------------------------------------------------------------------
# -> Users [[
# ------------------------------------------------------------------------------

# Add & change user uid
RUN useradd --shell /bin/bash -u 1024 -o -c "" -m devbox
RUN usermod -u 1000 devbox

USER devbox

# ]]
# ------------------------------------------------------------------------------
# -> Configure [[
# ------------------------------------------------------------------------------

# Set up uwsgi config list
COPY uwsgi /etc/uwsgi/

# Set up autoenv
RUN echo 'source `which activate.sh`' >> ~/.bashrc

# Set up virtual env wrapper
RUN echo 'export WORKON_HOME=$HOME/.virtualenvs' >> ~/.bashrc
RUN echo 'source /usr/local/bin/virtualenvwrapper.sh' >> ~/.bashrc

# Change working directory
WORKDIR /var/www/project

# ]]
# ------------------------------------------------------------------------------
