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

ARG ENABLE_PHP=false
# Copy: php sites [[
COPY if [ ${ENABLE_PHP} = true ]; then \
    sites/php /etc/nginx/conf.d \
;fi
# ]]

ARG ENABLE_PYTHON=false
# Copy: python sites [[
COPY if [ ${ENABLE_PYTHON} = true ]; then \
    sites/python /etc/nginx/conf.d \
;fi
# ]]

# ]]
# ------------------------------------------------------------------------------
