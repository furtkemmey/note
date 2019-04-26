# UBUNTU

# 預設啟動級別

## 開機後運行目標設定
    systemctl set-default 目標.target
    
## 現在設定的目標
    systemctl get-default
    
## 目標項目 圖形界面 或是文字界面
    multi-user.target
    graphical.target
    
## 不重啟切換
    systemctl isolate 目標.target
    
# 蓋上不休眠
- 新增

        /etc/systemd/logind.conf
            HandleLidSwitch=ignore        

- 重啟

        systemctl restart systemd-logind
        
# systemctl

## 啟動
    systemctl start 服務
## 關閉
    systemctl stop 服務
## 重啟
    systemctl restart 服務
## 重新載入設定檔
    systemctl reload 服務
## 下次開機啟動
    systemctl enable 服務
## 下次關機不啟動
    systemctl disable 服務
## 狀態
    systemctl status 服務
## 詢問目前有在運作嗎
    systemctl is-active 服務
## 詢問開機有沒有要啟動
    systemctl is-enabled 服務