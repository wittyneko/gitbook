# 软件问题处理

## Sysnergy2

### 失效重启

```bash
# Linux
sudo systemctl status synergy
sudo systemctl stop synergy
sudo systemctl start synergy
sudo systemctl restart synergy

# Mac
sudo pkill -f synergy
open /Applications/Synergy.app
killall synergy-config
killall synergy-core
killall synergy-tray
killall synergy-service
```

[Synergy 2 on Linux - Installs old version - General Discussion](https://symless.com/forums/topic/5212-synergy-2-on-linux-installs-old-version/)

[Synergy 2: How to uninstall and reinstall](https://symless.com/forums/topic/4519-synergy-2-how-to-uninstall-and-reinstall/)

<iframe src="https://plugins.gitbook.com/plugin/url-embed" style="width: 100%; height: 600px; border: 0px none;"></iframe>