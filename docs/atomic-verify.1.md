% ATOMIC(1) Atomic Man Pages
% Dan Walsh
% May 2015
# NAME
atomic-verify - Verify image is fully updated

# SYNOPSIS
**atomic verify**
[**-h**|**--help**]
[**-s**|**--sign**]
[**--sign-by**]
[**-v**|**--verbose**]
IMAGE

# DESCRIPTION
**atomic verify** does serveral checks of an image.

It checks whether there is a newer image available and scans
through all layers to see if any of the layers, which are base images themselves, have a new version available.
If the tool finds an out of date image, it will report as such.

If the image or any of its layers are pulled from a repository, it will attempt to check the repository
to see if there is a new image and capture any of its relevant information like version (where applicable).

Any images that do not possess a **Version** LABEL cannot be compared for available updates.  If an image
lacks the version information, it will still be part of the layer descriptions but will be cited as not having
the version information.

Verify also checks to see if the image is signed and the signature is trusted.

The default activity of Verify can also be overridden to create a signature
file indicating the "sing-by" user trusts the content of the image.

# OPTIONS:
**-h** **--help**
  Print usage statement
**-s** **--sign**
  Create a signature file indicating that this image is trusted by the signer of the image
**--sign-by**
  Select the signers identity to sign an image.  Default signer can be defined in the /etc/atomic.conf file.
**-v** **--verbose**
  Will output the status of each base image that makes up the image being verified.

# EXAMPLES
Verify the Red Hat rsyslog image

    # atomic verify registry.access.redhat.com/rhel7/rsyslog
    #
Verify the Red Hat rsyslog image and show status of each image layer

    # atomic verify -v registry.access.redhat.com/rhel7/rsyslog
    registry.access.redhat.com/rhel7/rsyslog contains the following images:

     rhel7/rsyslog-7.1-29           rhel7/rsyslog-7.1-29
     redhat/rhel7-7.1-24            redhat/rhel7-7.1-24

     * = version difference

# HISTORY
May 2015, Originally compiled by Daniel Walsh (dwalsh at redhat dot com)

Nov 2015, Updated for remote inspect by Brent Baude (bbaude at redhat dot com)

