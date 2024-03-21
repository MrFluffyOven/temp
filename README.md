# Sync a twrp minimal manifest, patch it for building OrangeFox, and sync the OrangeFox sources

## To fetch the manifest for the first time, follow these steps: ##
------------------------------------

### 1. Fetch these sync tools ###
	mkdir /home/j/foxsync; mkdir /home/maxim/foxbuild
	cd /home/j/foxsync
	git clone https://gitlab.com/OrangeFox/sync.git # (or, using ssh, "git clone git@gitlab.com:OrangeFox/sync.git")

### 2. Do the syncing (this can take up to 1 hour, and can use up to 40GB of disk space) - below is an example, for 12.1 (amend as required for other branches) ##
	cd /home/j/foxsync/sync/
	./orangefox_sync.sh --branch 12.1 --path /home/j/foxbuild
Notes:
- You *MUST* supply an *ABSOLUTE* path name for the "--path" switch
- If the sync process gets stuck, you might need to terminate it with Ctrl-C and then run the script again
- If you want to use ssh for cloning the OrangeFox sources and vendor tree, export "USE_SSH=1" before starting, or supply "--ssh 1" on the command line
- After the initial sync process, you must then clone your device trees, before you can build for your device

## These manifest branches are supported by the orangefox_sync.sh script: ##
----------------------------------
	12.1
	11.0

## To update the manifest, and the recovery sources, and the vendor trees (given the example of the 12.1 branch above), follow these steps: ##
----------------------------------
	cd /home/j/foxbuild
	repo sync # (ignore all errors and suggestions relating to "android_bootable_recovery")
	cd /home/j/foxbuild/bootable/recovery/
	git pull
	cd /home/j/foxbuild/vendor/recovery/
	git pull

## To update only the recovery sources (given the example of the 12.1 branch above), follow these steps: ##
----------------------------------
	cd /home/j/foxbuild/bootable/recovery/
	git pull

## To update only the vendor tree (given the example of the 12.1 branch above) follow these steps: ##
----------------------------------
	cd /home/j/foxbuild/vendor/recovery/
	git pull

## To update only the manifest (given the example of the 12.1 branch above), follow these steps: ##
----------------------------------
	cd ~/fox_12.1/
	repo sync # (ignore all errors and suggestions relating to "android_bootable_recovery")

## To see the syntax of the orangefox_sync.sh script, follow these steps: ##
----------------------------------
	cd ~/OrangeFox_sync/sync/
	./orangefox_sync.sh --help

