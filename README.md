# Instruqt Update Helper

This script performs 2 functions.

* Update the vm in each lab.
* Push the updated lab to instruqt.

The update operation will log the update in the instruqt.log file and make backups of the config file in backup/. If a mistake is made, you can also revert all changes through git.

## Instructions

### Activate the venv

```bash
source .venv/bin/activate
```

### Run the script on the cli

```bash
python Instruqtupdate.py
```

By default, the logging will be set to verbose and the changes will be destructive. Backups of the config.yml for each lab are created in the backup directory (specified in the config/instruqt.conf file).

This script can run in a non-destructive _check_ mode which compares the image key in the config.yml to the newvm key specified in the config/instruqt.conf file. To run a non-destructive check, run the following on the cli.

```bash
python Instruqtupdate.py --check
```

This will output the labs that are not up to date.

## Installation

Clone this repo. In this example, we're running `git clone` from `/home/myee/instruqt_dev/`.

```bash
git clone https://github.com/myee111/instruqt-update-helper.git /home/myee/instruqt_dev/
```

This script uses a venv.

```bash
virtualenv -p python3 /home/myee/instruqt_dev/instruqt-update-helper/
```

Activate the venv.

```bash
source /home/myee/instruqt_dev/instruqt-update-helper/bin/activate
```

Install the required python modules with pip.

```bash
pip install -r /home/myee/instruqt_dev/instruqt-update-helper/requirements.txt
```

## Configuration

The configuration file looks like this.

```ini
[general]
debug = True
log = instruqt.log
backupdir = backup

[instruqt]
instruqt_push_command = instruqt track push
instruqt_pull_command = instruqt track pull --force
instruqt_root_dir = /home/myee/test/instruqt
config_file_name = config.yml
labs: [
  "test",
  "unixisms",
  "openscap"
  ]

[oldimage]
image: projects/tmm-instruqt-11-26-2021/global/images/rhel-8-5-03-02-2022-1

[newimage]
image: projects/tmm-instruqt-11-26-2021/global/images/rhel-8-6-05-10-2022-1
