.. _operation:

Operation
=========

Nodepool generally runs as a daemon under the command ``nodepoold``.
Once started, it will frequently re-read the configuration file and
make any changes necessary (such as adding or removing a provider, or
altering image or quota configuration).  If any needed images are
missing, it will immediately begin trying to build those images.
Periodically (once a day by default but configurable in the ``cron:``
section of the config file) it will attempt to create new versions of
each image.

If a new image creation is successful, it will immediately start using
it when launching nodes (Nodepool always uses the most recent image in
the ``ready`` state).  Nodepool will delete images that are older than
8 hours if they are not the most recent or second most recent
``ready`` images.  In other words, Nodepool will always make sure that
in addition to the current image, it keeps the previous image around.
This way if you find that a newly created image is problematic, you
may simply delete it and Nodepool will revert to using the previous
image.

Metadata
--------

When nodepool creates instances, it will assign the following nova
metadata:

  groups
    A json-encoded list containing the name of the image and the name
    of the provider.  This may be used by the Ansible OpenStack
    inventory plugin.

  nodepool
    A json-encoded dictionary with the following entries:

    image_name
      The name of the image as a string.

    provider_name
      The name of the provider as a string.

    node_id
      The nodepool id of the node as an integer.

Command Line Tools
==================

Usage
-----
The general options that apply to all subcommands are:

.. program-output:: nodepool --help
   :nostderr:

The following subcommands deal with nodepool images:

dib-image-list
^^^^^^^^^^^^^^
.. program-output:: nodepool dib-image-list --help
   :nostderr:

image-list
^^^^^^^^^^
.. program-output:: nodepool image-list --help
   :nostderr:

image-build
^^^^^^^^^^^
.. program-output:: nodepool image-build --help
   :nostderr:

image-update
^^^^^^^^^^^^
.. program-output:: nodepool image-update --help
   :nostderr:

image-upload
^^^^^^^^^^^^
.. program-output:: nodepool image-upload --help
   :nostderr:

dib-image-delete
^^^^^^^^^^^^^^^^
.. program-output:: nodepool dib-image-delete --help
   :nostderr:

image-delete
^^^^^^^^^^^^
.. program-output:: nodepool image-delete --help
   :nostderr:

The following subcommands deal with nodepool nodes:

list
^^^^
.. program-output:: nodepool list --help
   :nostderr:

hold
^^^^
.. program-output:: nodepool hold --help
   :nostderr:

delete
^^^^^^
.. program-output:: nodepool delete --help
   :nostderr:

If Nodepool's database gets out of sync with reality, the following
commands can help identify compute instances or images that are
unknown to Nodepool:

alien-list
^^^^^^^^^^
.. program-output:: nodepool alien-list --help
   :nostderr:

alien-image-list
^^^^^^^^^^^^^^^^
.. program-output:: nodepool alien-image-list --help
   :nostderr:
