# PID AutoTune Plugin for CraftBeerPi 3.0

This plugin is a port of the PIDAutoTune logic from CraftBeerPi 2.2, with some added features to aid in usability. The purpose of autotuning is achieve a better set of variables to use for configuring your other PID-controlled devices, such as a heating element in your mash tun. Once you have used PIDAutoTune to calibrate your system, you will be given three numbers which you must enter into the settings page for the appropriate device. 

For more info on PID and autotuning, you can check out the following articles:
- https://github.com/Manuel83/craftbeerpi/wiki/Autotune-PID
- https://github.com/Manuel83/craftbeerpi/wiki/Manual-PID-adjustment

## Installation

1. Install the plugin by navigating to the **System** menu in CraftBeerPi 3.0 and then clicking **Add-On**.
2. Download the plugin and then reboot your Raspberry Pi

## Configuration

1. Click on the **System** menu and choose **Hardware Settings**.
2. If you do not have a kettle already created, click **Add** and create one first. Otherwise, click on the name of the kettle that you want to calibrate with autotune. 

:warning: ***NOTE:*** There is currently a bug in the GPIOPWM actor. If you are using this mode, you should switch to GPIOSimple for the time being if you want to use PIDAutoTune or PIDArduino.

3. Under the **Logic** drop-down menu, choose PIDAutoTune and then configure the following options:    
    1. **output step %**: defines the output of the autotune-algorithm when stepping up/down, e.g. output step = 100; step up (=heating) output = 100; step down (= cooling) output = -100. This setting should stay at 100%    
    2. **max. output %**: limits the maximum power output. This is useful if your heater is overpowered and would heat up the kettle way too fast. If you don't want to limit your heater, leave this at the default value of 100%
    3. **lookback seconds**: determines how far the algorithm will look back when trying to find local (temperature) extrema (minima/maxima). If the algorithm recognizes even short peaks as extrema, you should increase this value. If it doesn't recognize actual extrema, you should decrease it. Usually the default of 30 seconds work fine.
        - *Descriptions of settings from the CraftBeerPi Wiki*
    4. Click the **Update** button once your settings are entered.
4. Now we are ready to begin the autotune process. Navigate to the **Brewing** dashboard and turn on any pumps or agitators that you would normally be using with this kettle.
5. Change the set point for the kettle to a typical temperature, like one you would use for mashing.
6. Click the **Auto** ![auto](https://user-images.githubusercontent.com/29404417/27567034-3a429f70-5ab7-11e7-90ef-2ff21645febf.png) button for the kettle you want to calibrate and the autotuning process will commence.

![autotune1](https://user-images.githubusercontent.com/29404417/27567079-73b1450e-5ab7-11e7-9b34-537d75049d74.jpg)

7. The kettle heater will come on and bring the temperature up to the set point, and intentionally overshoot it. Then an oscillation will occur where the temp goes over and then back under the set temp many times. This process can take over an hour depending on many factors, so leave it be while it's calibrating.

:bulb: ***Tip***: If you want to actively watch  what autotune is doing, you can run the following command from your Raspberry Pi to see the live output: `tail -f ~/craftbeerpi3/logs/autotune.log`

8. When it's finished, the Auto mode will disable itself and you will see several notifications. These will give you the PID values for the primary "brewing" rule as defined by the autotune algorithm.

![autotune2](https://user-images.githubusercontent.com/29404417/27567047-4f682366-5ab7-11e7-8900-09473197996d.jpg)

9. Now you can navigate back to the **Hardware Settings** screen under the **System** menu, pick your kettle, and change the **Logic** setting to PIDArduino (or another PID-based plugin of your choice).
10. Copy and paste the PID values from the on-screen notifications into the fields on the settings page. Click **Update** when done.

![autotune3](https://user-images.githubusercontent.com/29404417/27567038-44cb81be-5ab7-11e7-94ac-b2934528dfa3.jpg)

## Log File

If there were any problems along the way, or you would like to see the other values and calculations that autotune determined for your system, you can click on the **System** menu, choose **Logs**, and then download the *autotune.log* file.
