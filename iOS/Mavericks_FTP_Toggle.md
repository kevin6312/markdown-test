在Mac OS X Mavericks 上，己經將原來放置在 "檔案共享"裡的 "FTP伺服器" 選項己經拿掉了。現在只能透過 command line 中的 launchctl 去啟動和關閉系統內建的"FTP伺服器"。

#### 開啟
    sudo -s launchctl load -w /System/Library/LaunchDaemous/ftp.plist


#### 關閉
    sudo -s launchctl unload -w /System/Library/LaunchDaemous/ftp.plist