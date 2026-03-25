To compile use following command on the raspberry pi for the sgtl5000 overlay.

dtc -@ -I dts -O dtb -o sgtl5000-audio.dtbo sgtl5000-audio-overlay.dts


Copy compiled binary sgtl5000-audio.dtbo into /boot/overlays

Add the entry
dtoverlay=sgtl5000-audio
in /boot/config.txt
