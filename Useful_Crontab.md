# Useful Crontab


## User
```
@reboot rm -rf ~/.cache/pip/http/*
@reboot rm -rf ~/.cache/google-chrome/Default/Cache/*
@reboot rm -rf  ~/.cache/thumbnails/*/*
@reboot rm -rf ~/.cache/mozilla/firefox/*
@reboot rm -rf ~/.cache/pip/wheels/*
```

## Root
```
@reboot echo deep > /sys/power/mem_sleep
@reboot sed -i 's/Exec=firefox/Exec=env MOZ_USE_XINPUT2=1 firefox/g' $(locate firefox.desktop)
```

Fixing AMD turbo boost
```
* * * * * echo 1 > /sys/devices/system/cpu/cpufreq/boost
```
