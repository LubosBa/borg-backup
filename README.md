# borg-backup
This repository contains Bash wrapper scripts made around backup software called [Borg](https://www.borgbackup.org/).

## Project structure.
Since this repository only contains the main scripts and not full project structure, the structure should be created manually.
Here is an example of the required folder structure:

```
.
├── bin
├── conf
├── README.md
├── storage
└── tmp
```

## Usage
`./bin` - folder contains all the wrapper scripts and main configuration of borg.  
`./bin/env` - file controls some of the configuration of Borg.

## borg-init
This script will create Borg repository for backup purposes. As a first argument it takes destination of repository which is relative to `STORAGE` variable
set in `bin/env` configuration file.  
Make sure that the repository name corresponds with the name of docker container that is being backed up.

Command example:
```
borg-init folder/repository-name
```

## borg-create
This script will create a backup of data into it's repository. The script takes one argument, the backup category, currently following categories are supported:

* docker-fpm
  * This category contains backups of FPM docker instances that are run on the backup host.
  * Following folders are included in the backup repository: `${DOCKERBASE}/conf/${BASENAME}` and `${DOCKERBASE}/data/webs1.m8.sk/${BASENAME}`
* static-html
  * This category contains backups of static content of various websites that are hosted on nginx docker container.
  * Following folders are included in the backup repository: `${DOCKERBASE}/data/webs1.m8.sk/${BASENAME}`
* docker
  * This category contains backups of general purpose docker containers.
  * Following folders are included in the backup repository: `${DOCKERBASE}/data/${BASENAME}` and `${DOCKERBASE}/conf/${BASENAME}`
