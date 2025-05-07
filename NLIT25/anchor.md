# Anchor - DevOps Focused Boot Management for HPC

Anchor is a framework for creating and deploying HPC root FS images using OCI container

1. Builds a base container
2. Extracts the kernel and initrd from base
3. Creates a new container in which Puppet is run to customize the image
4. Creates a squashFS root FS from the second container, which is then used as the system image

Old repo: https://github.com/olcf/anchor Lots of work done since then
