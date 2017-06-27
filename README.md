# PID AutoTune plugin for CraftBeerPi 3.0

This plugin is a port of the PIDAutoTune logic from CraftBeerPi 2.2, with some added features to aid in usability. The purpose of autotuning is achieve a better set of variables to use for configuring your other PID-controlled devices, such as a heating element in your mash tun. Once you have used PIDAutoTune to calibrate your system, you will be given three numbers which you must enter into the settings page for the appropriate device. 

For more info on PID and autotuning, you can check out the following articles:
- https://github.com/Manuel83/craftbeerpi/wiki/Autotune-PID
- https://github.com/Manuel83/craftbeerpi/wiki/Manual-PID-adjustment

## Installation

1. Install the plugin by navigating to the **System** menu in CraftBeerPi 3.0 and then clicking **Add-On**.
2. Download the plugin and then reboot your Raspberry Pi
3. Click on the **System** menu and choose **Hardware Settings**.
4. If you do not have a kettle already created, click **Add** and create one first. Otherwise, click on the name of the kettle that you want to calibrate with autotune.
5. Under the **Logic** drop-down menu, choose PIDAutoTune and then configure the following options:    
    1. **output step %**: defines the the output of the autotune-algorithm when stepping up/down, e.g. output step = 100; step up (=heating) output = 100; step down (= cooling) output = -100. This setting should stay at 100%    
    2. **max. output %**: limits the maximum power output. This is useful if your heater is overpowered and would heat up the kettle way too fast. If you don't want to limit your heater, leave this at the default value of 100%
    3. **lookback seconds**: determines how far the algorithm will look back when trying to find local (temperature) extrema (minima/maxima). If the algorithm recognizes even short peaks as extrema, you should increase this value. If it doesn't recognize actual extrema, you should decrease it. Usually the default of 30 seconds work fine.
    4. Click the **Update** button once your settings are entered.
    - *Settings descriptions from CraftBeerPi Wiki*
6. Now we are ready to begin the autotune process. Navigate to the Brewing dashboard and turn on any pumps or agitators that you would normally be using with this kettle.
7. Change the set point for the kettle to a typical temperature, like one you would use for mashing.
8. Click the **Auto** button for the kettle you want to calibrate and the autotuning process will commence.
7. The kettle heater will come on and bring the temperature up to the set point, and intentionally overshoot it. Then an oscilation will occur where the temp goes over and then back under the set temp many times. This process can take over an hour depending on many factors, so leave it be while it's calibrating.
8. When it's finished, the Auto mode will disable itself and you will see several notifications. These will give you the PID values for the primary "brewing" rule as defined by the autotune algorithm.
