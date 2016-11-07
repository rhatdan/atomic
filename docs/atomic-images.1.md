% ATOMIC(1) Atomic Man Pages
% Dan Walsh
% July 2015
# NAME
atomic-images - operations on container images

# SYNOPSIS
**atomic images COMMAND [OPTIONS] [IMAGES...]**

atomic images allows the user to view and operate on container images in a docker registry.

# COMMANDS
**list**

  List all installed container images on your system.

  A  **>** preceding the image name indicates that the image is used by a container.

  A **\*** in the first column indicates a dangling image. **Dangling** images are images with no name/tag and which are not used by any other images. Since they are not used, they waste system space.  Dangling images can be caused by using 'docker build' to update an image without removing the older version of the image.

**delete**

  Delete the specified container image(s). If you use the **--remote option** remote disk space will not be freed until the **registry garbage-collection** command is invoked for the remote registry.

**info**

  Displays the LABEL fields within an image. By default, it will check first for a local image and then all configured registries.

**help**

  Displays a help file associated with a container or image.

  If a container or image has a help file (in man format) embedded in itself, atomic help will display the help file in a pager similar to man.  The default location for a help file is /image_help.1 but the location of the help can be overridden with the HELP LABEL.  If you choose to override the default location, ensure the path provided is a fully-qualified path that includes the help file itself.

  The help file can be written using the middleman markup and the converted using the go-md2man utility as follows:
```
go-md2man -in image_help.1.md -out image_help.1
```
You can also use any of the many options to create the help file including using native man tagging.

**prune**

  Prune/delete all **dangling** images, freeing wasted disk space.

**verify**
  Checks whether there is a newer image available and scans through all layers to see if any of the layers, which are  base  images themselves,  have a new version available.  If the tool finds an out of date image, it will report as such. If the image is a system image,  it will  also look through the layers and validate each layer to determine if it has been tampered with and output details of these changes (if at all).

  If the image or any of its layers are pulled from a repository, it will attempt to check the repository to see if there is a new image and capture any of its relevant information like version (where applicable).

  Any  images  that do not possess a Version LABEL cannot be compared for available updates.  If an image lacks the version information, it  will still be part of the layer descriptions but will be cited as not having the version information.

**version**
  Display image 'Id Name:Version:Release RepoTag' label

# delete OPTIONS
[**-h|--help**]
  Print usage statement

[**-f|--force**]
  Force the deletion of specified local images, even if they are in use.

[**--remote**]
  Delete images in remote registry.  *--force* is not supported with this option.

[**--storage=[ostree|docker]**]
  Optionally specify the storage from which to delete the image from. Will prompt user to specify if the same image name exists in both ostree and docker, and the user did not specify.

# Note:
Atomic --assumeyes option can be used

[**-y|--assumeyes**]
  Delete image(s) without conformation from the user

# info OPTIONS
[**-h|--help**]
  Print usage statement

[**--remote**]
  Ignore all local images, only search configured registries.

[**--storage=[ostree|docker]**]
  Optionally specify the storage of the image. Will prompt user to specify if the same image name exists in both ostree and docker, and the user did not specify.

# list OPTIONS
[**-h|--help**]
  Print usage statement

[**-a|--all**]
  Show all images, including intermediate images

[**-f|--filter**]
  Filter output based on given filters, example usage: '--filter repo=foo'
will list all images that has "foo" as part of their repository name.

[**-n|--noheading**]
  Do not print heading when listing the images

[**--no-trunc**]
  Do not truncate output

[**-q|--quiet**]
  Only display image IDs

[**--json**]
  Output in the form of JSON.

# verify OPTIONS

[**-h|--help**]
  Print usage statement

[**--no-validate**]
  Skip validation of the files contained inside the image.

[**--storage=[ostree|docker]**]
  Optionally specify the storage of the image. Will prompt user to specify if the same image name exists in both ostree and docker, and the user did not specify.

[**-v|--verbose**]
   Will output the status of each base image that makes up the image being verified.

# version OPTIONS
[**-h|--help**]
  Print usage statement

[**-r|--recurse**]
  Recurse through all layers of the specified image.

[**--storage=[ostree|docker]**]
  Optionally specify the storage of the image. Will prompt user to specify if the same image name exists in both ostree and docker, and the user did not specify.

# EXAMPLES
Verify the Red Hat rsyslog image

    # atomic images verify registry.access.redhat.com/rhel7/rsyslog
    #
Verify the Red Hat rsyslog image and show status of each image layer

    # atomic images verify -v registry.access.redhat.com/rhel7/rsyslog
    registry.access.redhat.com/rhel7/rsyslog contains the following images:

     rhel7/rsyslog-7.1-29           rhel7/rsyslog-7.1-29
     redhat/rhel7-7.1-24            redhat/rhel7-7.1-24

     * = version difference
Verify a system image

    # sudo atomic images verify busybox
    validation output for layer a3ed95caeb02ffe68cdd9fd84406680ae93d633cb16422d00e8a7c22955b46d4:

	(no changes detected)

    validation output for layer 8ddc19f16526912237dd8af81971d5e4dd0587907234be2b83e249518d5b673f:

    "etc/shadow": keyword "size": expected 243; got 268
    "etc/shadow": keyword "sha256digest": expected 22d9cee21ee808c52af44ac...; got 7a07ac69054c2a3533569874c2...

# HISTORY
July 2015, Originally compiled by Daniel Walsh (dwalsh at redhat dot com)
July 2016, Updated to reflect images sub-command changes (jhonce at redhat dot com)
July 2016, Added sub-commands all, filter and quiet to list (jerzhang at redhat dot com)
