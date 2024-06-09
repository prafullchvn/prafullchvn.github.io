---
title: "Multi architecture management in Colima"
date: 2024-06-09T20:44:31+05:30
draft: false
tags:
    - docker
    - colima
    - aarch64
---


### Multi-profiles management

One of the most exciting Colima features is instances management. To do so, Colima is using profiles.

To create an instance with a profile name, add the `-p` flag to the command line. For example, `colima start -p funny_profile` will create a default instance with`funny_profile`as profile name.`colima start -p intel -a x86_64 -c 1`will start an intel instance with 1 CPU using the`intel`name.

You can retrieve your current profiles by running `colima list`.


```
PROFILE          STATUS     ARCH       CPUS    MEMORY    DISK     RUNTIME    ADDRESS
default          Stopped    aarch64    2       2GiB      60GiB
funny_profile    Running    aarch64    2       2GiB      60GiB    docker
intel            Running    x86_64     1       8GiB      60GiB    docker

```

> Note: Profile name must be unique. If the name is not given when starting an instance,defaultwill be the default name.
>

To stop your instance, run`colima stop`with`-p <PROFILE>`*(<PROFILE> is your instance name).*To delete a profile, run`colima delete`with`-p <PROFILE>`.

### Editing an instance

It is possible to customize an instance before starting it using flags, or by running the`start`command with the`-e`flag. Your terminal editor will open the instance configuration file to be edited. After modification, the instance will start.

> Note: Once created, each configuration property is editable except the disk size.
>

### Multi-architecture management

The second great feature of Colima is the CPU architecture emulation (i.e. aarch64, x86_64), available with the`-a`flag. Let's say you got an M1 laptop and the desired docker image does not have an aarch64 version. By switching or creating a specific amd64 instance, you will be able to run the image.

```
# Default with Intel architecture
colima start -a x86_64
# Default with arm architecture
colima start -a aarch64
```

### For m1

creating profile

```bash
colima start -p native -a aarch64 --cpu 8 --disk 120 --memory 20
```

### Build image using this platform

`docker build --platform linux/arm64`