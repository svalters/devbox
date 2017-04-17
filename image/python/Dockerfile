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
# -> Install Python packages [[
# ------------------------------------------------------------------------------

RUN pip install \
    uwsgi \
    virtualenv \
    autoenv

# ]]
# ------------------------------------------------------------------------------
# -> Configure [[
# ------------------------------------------------------------------------------

# Set up uwsgi config list
COPY uwsgi /etc/uwsgi

# Change working directory
WORKDIR /var/www/project

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
# -> Environments [[
# ------------------------------------------------------------------------------

# Create tmp dir
RUN mkdir ~/tmp

# Set up autoenv
RUN echo 'source `which activate.sh`' >> ~/.bashrc

# Set up virtual env wrapper
RUN echo 'export WORKON_HOME=$HOME/.virtualenvs' >> ~/.bashrc
RUN echo 'source /usr/local/bin/virtualenvwrapper.sh' >> ~/.bashrc

# ]]
# ------------------------------------------------------------------------------
