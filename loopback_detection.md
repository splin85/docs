# Loopback detection
## 命令
    loopback-detect enable 
        使能所有接口的loopback detect功能，系统视图
        使能单个接口的loopback detect功能，接口视图
        
    loopback-detect packet vlan { vlan-id1 [ to vlan-id2 ] } &<1-8>
        配置对指定的vlan进行检测，接口视图 
        
    loopback-detect untagged mac-address mac-address
        配置检测报文的mac地址，系统视图
       
    loopback-detect packet-interval packet-interval-time
        配置检测报文的发送周期 ，系统视图
        
    loopback-detect action { block | nolearn | shutdown | trap | quitvlan }
        配置检测到环路后，对接口的处理动作，接口视图
        
    loopback-detect recovery-time recovery-time
        配置环回消失后接口都自动恢复的时间，接口视图
        
    display loopback-detect
        查看环回检测情况