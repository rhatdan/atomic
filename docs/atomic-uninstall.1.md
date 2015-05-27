% ATOMIC(1) Atomic Man Pages
% Dan Walsh
% January 2015
# NAME
atomic-uninstall - Remove/Uninstall container/container image from system

# SYNOPSIS
**atomic uninstall**
[**-f**][**--force**]
[**-h**]
IMAGE [ARG...]

# DESCRIPTION
**atomic uninstall** attempts to read the `LABEL UNINSTALL` field in the
container IMAGE, if this field does not exists **atom uninstall** will just
uninstall the image.

If the container image has a LABEL UNINSTALL instruction like the following:

```LABEL UNINSTALL /usr/bin/docker run -t -i --rm --privileged -v /:/host --net=host --ipc=host --pid=host -e HOST=/host -e NAME=\${NAME} -e IMAGE=\${IMAGE} -e CONFDIR=\${CONFDIR} -e LOGDIR=\${LOGDIR} -e DATADIR=\${DATADIR} --name NAME IMAGE /bin/uninstall.sh \${NAME}.config```

`atomic uninstall` will replace the NAME, ${NAME}, IMAGE and ${IMAGE} fields
with the name and image specified via the command,  `atomic uninstall` will
also pass in the CONFDIR, LOGDIR and DATADIR environment variables to the
container. Any additional arguments will be appended to the command.

# OPTIONS:
**-f** **--force**
  Remove all containers based on this image

**--help**
  Print usage statement

**--name**=""
   If name is specified `atomic uninstall` will uninstall the named container from the system, otherwise it will uninstall the container images.

# HISTORY
January 2015, Originally compiled by Daniel Walsh (dwalsh at redhat dot com)
