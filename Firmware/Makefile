## Which device the steam controller shows up as when you plug it in with the right trigger held.
device=/dev/sdb
bin=OpenSteamController/Debug/OpenSteamController.bin
mountpt=build/mnt
backups=build/backup

## Mount the steam controller somewhere
.PHONY: mount
mount:
	mkdir -p $(mountpt)
	if ! mountpoint $(mountpt) ; then sudo mount $(device) $(mountpt) ; fi

## Copy the existing firmware on the controller to a backup
.PHONY: backup
backup: mount
	mkdir -p $(backups)
	dd if=$(mountpt)/firmware.bin of=$(backups)/firmware-$(shell date +%s).bin

$(bin):
	if [ ! -f $(bin) ] ; then printf "\n***\nYOU MUST FIRST BUILD THE FIRMWARE USING LPCXpresso\n***\n" ; exit 1 ; fi

flash: mount $(bin)
	dd conv=nocreat,notrunc oflag=direct bs=512 if=$(bin) of=$(mountpt)/firmware.bin

