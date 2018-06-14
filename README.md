# CPUProfiles
Messing around with cpu profiles 

**Original documentation:** https://tinyurl.com/yb2n8z5s
<details> 
  <summary>INTERACTIVE GOVERNOR</summary>

___
# timer_slack

The amount of time in miliseconds; that the cpu will stay in the highest frequency before it applies "interactive" tunings again

*Basically, if there is a cpu intensive application and you have a high cpu load; timer_slack delays ramping down to lower frequencies in a given "X" time. Also, since timer_rate will be erratic, this should help to decrease stutters.*

**_higher value: higher battery drain, better performance_**
___

# timer_rate

The amount of time in miliseconds; that the cpu will check how heavy the cpu load is.

*E.g. if you have set this to 20000, it'll compute every 20ms to see if any changes on the cpu load is making and will therefore adjust the frequency based on target_loads.*

**_higher value: less battery drain, performance impact subjective_**
___

# target_loads

The amount of load, in theory on percentage; where the actual frequency should be used. 

*Target_loads can be setup per frequency to provide certain "bias" on cpu clocks. An example "35 475600:88 600000:21 960000:98" means that anything before 475Mhz would have a target load of 35%. At 475Mhz before ramping up there should be at least 88% of cpu load, once this threshold is broken it'll ramp up to 960Mhz immediately since 600Mhz is set less than 475Mhz. Therefore the two "bias" created on the sample above is 475Mhz and 960Mhz. It is not recommended to provide any values higher than 98 as this will reduce performance on your cat greatly*

**_Higher value: less battery drain, worse performance_**
___

# min_sample_time
The minimum amount of time the governor must wait at a given frequency until it can decide to reduce the frequency.

**_higher value: better performance, battery impact HIGHLY subjective_**
___

# hispeed_freq
This would be the frequency that the user "assumes" would be enough to handle a boost in cpu load. 

*Too high value would greatly impact the user's UI performance but would definitely worsen the battery life.*

**_higher value: higher battery drain, better performance_**
___

# go_hispeed_load
The load assigned to the cpu where it is recommended to go to the hispeed_freq. 

*Set this quite high as this bypass almost everything in the interactive tunables.*

**_higher value: less battery drain, performance impact subjective_**
___


# above_hispeed_delay
A delay setup in frequency:miliseconds to slow down and "delay" aggressive ramp ups.

*E.g. 19000 600000:24000; provides 19ms delay to cpu frequencies not specified after reaching hispeed_frequency, before ramping up to a higher frequency. If, for example you have your hispeed_frequency set up to 960Mhz, and your above hispeed_delay to 30000 1248000:22000 1354000:40000; the 30ms will only be used at 960Mhz up until 1248Mhz where the delay is 22000. Please note that 30000(30ms) from the example above will NOT BE APPLIED to all frequencies BELOW the set hispeed_frequency (anything below 960Mhz). Also, specified "frequency:delay" ratios should be written in ascending order according to cpufreq linux documentations.*
**_higher value: less battery drain, worse performance_**
___


# align_windows
With the value of "1" for On and "0" for Off. If "1" is designated, the cluster for cpu clocks (divided into big and little) will fire at short quick intervals, usually by 1ms to provide a reliable boost to what timer_rate has converted cpu loads/clocks into.

**_If ON: better performance_**
___


# max_freq_hysteresis
Checks the cpu for "hysteresis" or previous cpu clock records and base the next ramp up on frequencies previously used. 

*If your cpu tends to have a bias towards lower cpu clocks, with this on a high value; it should frequently stick to lower cpu frequencies.*

**_higher value: less battery drain, performance impact subjective_**
___


# powersave_bias
Value of "1" to turn ON and "0" for OFF. If your cpu decides to go for 960mhz, with powersave_bias ON it'll go to a frequency one step below 960mhz.


**_urn ON: less battery drain, worse performance_**
___


# use_migration_notif
Value of "1" for ON and "0" for OFF. Reevaluate the cpu frequency if "notified" (unclear, we can assume this as either an unschedule app notification or a "timed" boost) to fire in 1ms. This aids timer_rate in quick changes with system loads.

**_Turn ON: better performance, battery impact subjective_**
___


# ignore_hispeed_on_notif
Value of "1" for ON and "0" for OFF. Ignores the hispeed_load, hispeed_frequency and above_hispeed_delay once a cpu is "notified".

*Therefore, if a cpu is "notified" if this is set to "1" the cpu can ramp up to frequencies computed by timer_rate without any delays coming from hispeed frequency logic.*

**_Turn ON: heavy battery drain_**
___


# fast_ramp_down
Value of "1" for ON and "0" for OFF. Ignores min_sample_time which provides delay on cpu frequencies in miliseconds.

*This holds true ONLY if a cpu is "notified" and therefore avoids unreliable "bias" on certain clocks due to quick shift of cpu loads.*

**_Turn ON: less battery drain, performance impact HIGHLY subjective_**
___
</details>








