# tinkerboard_V1_pwmFanControl_DietPi
This is the updated script to control a 3 wire fan mounted on v1 tinkerboard and controlled for speed for those who love cooling on demand.

I've switched to dietPi because of its lean build on original Asus tinkerboard.
While the SBC is quite powerful, it needs lots of power and cooling. see https://github.com/karunakar2/tinkerBoard_simpleFanControl
While short cable length is the solution of the old 5v charger pin with a decent charger (the cable resistance works against the voltage) to maintain necessary voltage,
There are few things dietpi offers, throttling cpu freq, under balanced modes under cpu-governer setting.
While it caters to the purpose, the cpu junction temperature can still run hot, the known issue with v1 board.
Any 3 cable fan, with blue cable patched onto pwm3, port 32 might come to rescue when running randomly high loads.
https://www.asus.com/uk/networking-iot-servers/aiot-industrial-solutions/all-series/tinker-board/
However dietpi natively isn't configured for these ports as pwm
The solution is to update /boot/dietpiEnv.txt
See the entry of overlays, usually its loaded with uart2, swap it to pwm3.
reboot and the pwm3 should be visible under /sys/class/pwm/ as chip1 or 2.
Using python-periphery module the duty cycle can be set. https://python-periphery.readthedocs.io/en/latest/pwm.html

The script is updated to check cpu temperature and scale the fan speed up, shut down the machine if temp goes beyond threshold.

cheers
