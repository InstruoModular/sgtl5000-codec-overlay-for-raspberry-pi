To compile use following command on the raspberry pi for the sgtl5000 overlay.

dtc -@ -I dts -O dtb -o sgtl5000-audio.dtbo sgtl5000-audio-overlay.dts


Copy compiled binary sgtl5000-audio.dtbo into /boot/overlays

Add the entry
dtoverlay=sgtl5000-audio
in /boot/config.txt


this overlay assumes external clock MCLK (1.228 MHz) and that chip is constantly powered:

	fragment@0 {
		target-path = "/";
		__overlay__ {
			sgtl5000_3v3: sgtl5000_3v3 {
				compatible = "regulator-fixed";
				regulator-name = "sgtl5000-3v3";
				regulator-min-microvolt = <3300000>;
				regulator-max-microvolt = <3300000>;
				regulator-always-on;
				regulator-boot-on;
			};
		};
	};

	fragment@1 {
		target-path = "/";
		__overlay__ {
			sgtl5000_mclk: sgtl5000_mclk {
				compatible = "fixed-clock";
				#clock-cells = <0>;
				clock-frequency = <12288000>;
			};
		};
	};
