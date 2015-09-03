% ATOMIC(1) Atomic Man Pages
% Dan Walsh
% January 2015
# NAME
atomic-install - Execute Image Install Method

# SYNOPSIS
**atomic install**
[**-h**|**--help**]
[**--display**]
[**-n**][**--name**[=*NAME*]]
[**--opt1**[=*OPT*]]
[**--opt2**[=*OPT*]]
[**--opt3**[=*OPT*]]
IMAGE [ARG...]

# DESCRIPTION
**atomic install** attempts to read the `LABEL INSTALL` field in the container
IMAGE, if this field does not exist, `atomic install` will install the IMAGE.

If the container image has a LABEL INSTALL instruction like the following:

`LABEL INSTALL /usr/bin/docker run -t -i --rm \${OPT1} --privileged -v /:/host --net=host --ipc=host --pid=host -e HOST=/host -e NAME=\${NAME} -e IMAGE=\${IMAGE} -e CONFDIR=\/etc/${NAME} -e LOGDIR=/var/log/\${NAME} -e DATADIR=/var/lib/\${NAME} \${IMAGE} \${OPT2} /bin/install.sh \${OPT3}`

`atomic install` will set the following environment variables for use in the command:

**NAME**
  The name specified via the command.  NAME will be replaced with IMAGE if it is not specified.

**IMAGE**
  The name and image specified via the command.

**OPT1, OPT2, OPT3**
  Additional options which can be specified via the command.

**SUDO_UID**
  The `SUDO_UID` environment variable.  This is useful with the docker `-u` option for user space tools.  If the environment variable is not available, the value of `/proc/self/loginuid` is used.

**SUDO_GID**
  The `SUDO_GID` environment variable.  This is useful with the docker `-u` option for user space tools.  If the environment variable is not available, the default GID of the value for `SUDO_UID` is used.  If this value is not available, the value of `/proc/self/loginuid` is used.

Any additional arguments will be appended to the command.

# OPTIONS:
**-h** **--help**
  Print usage statement

**--display**
  Display the image's install options and environment variables populated into the install command.
The install command will not execute if --display is specified.
If --display is not specified the install command will execute.

**-n** **--name**=""
   Use this name for creating installed content for the container.
NAME will default to the IMAGENAME if it is not specified.

**--opt1**=""
   Substitute options specified as opt1 for all instances of ${OPT1} specified
in the LABEL.

**--opt2**=""
   Substitute options specified as opt2 for all instances of ${OPT2} specified
in the LABEL.

**--opt3**=""
   Substitute options specified as opt3 for all instances of ${OPT3} specified
in the LABEL.

# HISTORY
January 2015, Originally compiled by Daniel Walsh (dwalsh at redhat dot com)
July 2015, edited by Sally O'Malley (somalley at redhat dot com)
