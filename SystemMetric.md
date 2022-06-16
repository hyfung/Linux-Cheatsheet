# Ubuntu System Metric Guide (Bash)

## System-wide Variable

### System Uptime
Real time:  `cat uptime | cut -d ' ' -f 1`  
CPU time:   `cat uptime | cut -d ' ' -f 2`  
```
/proc/uptime
```
### /etc
|Subject|Location|
|-------|--------|
|Hostname|`/etc/hostname`|
|System Timezone|`/etc/timezone`|  
|Users in system|`/etc/passwd`|  
|Groups in system|`/etc/group`|  
|Filesystem table|`/etc/fstab`|
\
Show groups of current user: `groups`

## CPU Related

### Core count
`ls /sys/devices/system/cpu/cpufreq | wc -l`
```
/sys/devices/system/cpu/cpufreq
```

### CPU Current frequency (Per-core)
`cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_cur_freq`
```
/sys/devices/system/cpu/cpu*/cpufreq/scaling_cur_freq
```

### Min and Max CPU Freq
```
/sys/devices/system/cpu/cpu0/cpufreq/scaling_min_freq
/sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq
```

### Power Mode (Intel Only)
Getting power settings  
`cat /sys/devices/system/cpu/cpu0/cpufreq/energy_performance_available_preferences`  
`cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors`  
```
/sys/devices/system/cpu/cpu*/cpufreq/energy_performance_available_preferences
/sys/devices/system/cpu/cpu*/cpufreq/scaling_available_governors
```

Setting Governors (performance/powersave)
```bash
echo $GOVERNOR | sudo tee 
echo {performance|powersave} | sudo tee 
```

Setting Preferences (performance/balance_performance/balance_power/power)
```bash
echo $PREFERENCE | sudo tee 
echo {performance|balance_performance|power} | sudo tee 
```

Toggling Turbo-boost
```bash
 echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo
 echo 0 > /sys/devices/system/cpu/cpufreq/boost
```

### Power Mode (AMD Only)
Getting power settings  
` `  
` `  
```
/sys/devices/system/cpu/cpu*/cpufreq/energy_performance_available_preferences
/sys/devices/system/cpu/cpu*/cpufreq/scaling_available_governors
```

Setting Governors (performance/powersave)
```bash
echo $GOVERNOR | sudo tee 'scaling_available_governors'
```

Setting Preferences (performance/balance_performance/balance_power/power)
```bash
echo $PREFERENCE | sudo tee 'energy_performance_available_preferences'
```

## Memory Related

### vmstat (Virtual Memory Statistics)

|Swap|Free|Buff|Cache|Swap In|Swap Out|IO In|IO Out|
|---|---|---|---|---|---|---|---|
|3|4|5|6|7|8|9|10|

|Sys Intr|Sys CS|User|System|Idle|IOWait|Steal|
|---|---|---|---|---|---|---|
|11|12|13|14|15|16|17|

```bash
vmstat | tail -n 1 | cut -d ' ' -f ${INDEX}
```

### iostat (CPU Statistics)
|User|Nice|System|IOWait|Steal|Idle|
|---|---|---|---|---|---|
|1|2|3|4|5|6|
```bash
iostat | head -n 4 | tail -n 1 | cut -d ' ' -f ${INDEX}
```

## IO Related

### 123
```

```

### 123
```

```

## Power Related

### HP x360
```
hwmon0: AC
    Online:     /sys/class/hwmon/hwmon0/device/online
hwmon1: ACPI

hwmon2: BAT0
    Battery%:   /sys/class/hwmon/hwmon2/device/capacity
    Status:     /sys/class/hwmon/hwmon2/device/status
    Charge:     /sys/class/hwmon/hwmon2/device/charge_now
    Voltage:    /sys/class/hwmon/hwmon2/device/voltage_now
    Current:    /sys/class/hwmon/hwmon2/device/current_now
hwmon3: NVME
    Temp:       /sys/class/hwmon/hwmon3/device/temp1_input
hwmon4: PCH_SKYLAKE
    PCH T:      /sys/class/hwmon/hwmon4/temp1_input
hwmon5: WACOM
    N/A
hwmon6: CORETEMP
    Package:    /sys/class/hwmon/hwmon6/temp0_input
    Core:       /sys/class/hwmon/hwmon6/temp*_input
hwmon7: IWLWIFI-1
    Package:    /sys/class/hwmon/hwmon7/temp1_input
```

### X270
```
hwmon0: 
hwmon1: 
hwmon2: 
hwmon3: 
hwmon4: Thinkpad
    Fan RPM:    /sys/class/hwmon/hwmon4/fan1_input
hwmon5: 
hwmon6: 
```

# Tools Configuration Location

## Apache2
Sites Location: `/var/www`  
Conf Location: `/etc/apache2`  

## Apt
apt: `/etc/apt`  

## Docker

## Fail2ban
fail2ban: `/etc/fail2ban`  

## InfluxDB

## MongoDB

## MySQL
Database Location: `/var/lib/mysql/${DB_NAME}`  
Conf Location: `/etc/mysql/conf.d`  

## Nginx
Sites Location: ` `  
Conf Location: `/etc/nginx`  

## PHP
## Redis
## Samba
Conf Location: `/etc/samba`  

