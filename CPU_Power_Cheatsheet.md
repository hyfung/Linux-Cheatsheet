# CPU and Power Management

#### CPU Frequencies
|Subject            |Path                                                   |
|-------------------|-------------------------------------------------------|
|Current Frequency  |/sys/devices/system/cpu/cpu*/cpufreq/scaling_cur_freq  |
|Max Frequency      |/sys/devices/system/cpu/cpu*/cpufreq/cpuinfo_max_freq  |
|Base Frequency     |/sys/devices/system/cpu/cpu*/cpufreq/base_frequency    |
|Min Frequency      |/sys/devices/system/cpu/cpu*/cpufreq/cpuinfo_min_freq  |

#### CPU Frequency Scaling
|Subject                    |Path                                                               |Options                                                                            |
|-                          |-                                                                  |-                                                                                  |
|Scaling Governor (AMD)     |/sys/devices/system/cpu/cpu*/cpufreq/scaling_governor              |conservative<br>**ondemand**<br>userspace<br>powersave<br>performance<br>schedutil |
|Scaling Governor (Intel)   |/sys/devices/system/cpu/cpu*/cpufreq/scaling_governor              |performance<br>**powersave**                                                       |
|Power Preference (Intel)   |/sys/devices/system/cpu/cpu*/cpufreq/energy_performance_preference |default<br>performance<br>**balance_performance**<br>balance_power<br>power        |

#### Turbo Boost
|Platform   |Location                                       |Flag                       |
|-          |-                                              |-                          |
|Intel      |/sys/devices/system/cpu/intel_pstate/no_turbo  |0: Enabled<br>1: Disabled  |
|AMD        |/sys/devices/system/cpu/cpufreq/boost          |0: Disabled<br>1: Enabled  |

#### Enabling/Disabling CPU
Enabling:
> `echo 1 | sudo tee /sys/devices/system/cpu/cpu*/online`

Disabling:
> `echo 1 | sudo tee /sys/devices/system/cpu/cpu*/online`

####
