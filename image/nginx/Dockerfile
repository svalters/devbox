# vim: set foldmarker=[[,]] foldlevel=0 foldmethod=marker spell:
# ------------------------------------------------------------------------------
# -> Base image [[
# ------------------------------------------------------------------------------

FROM nginx:alpine

# ]]
# ------------------------------------------------------------------------------
# -> Configure [[
# ------------------------------------------------------------------------------

COPY config/nginx.conf /etc/nginx/nginx.conf
COPY ssl /etc/nginx/ssl

# Create & copy all available site list
RUN mkdir /etc/nginx/sites-available
COPY sites /etc/nginx/sites-available

ARG ENABLE_PHP=false
# Copy: php sites [[
RUN if [ ${ENABLE_PHP} = true ]; then \
    cp /etc/nginx/sites-available/php/* /etc/nginx/conf.d \
;fi
# ]]

ARG ENABLE_PYTHON=false
# Copy: python sites [[
RUN if [ ${ENABLE_PYTHON} = true ]; then \
    cp /etc/nginx/sites-available/python/* /etc/nginx/conf.d \
;fi
# ]]

# ]]
# ------------------------------------------------------------------------------
