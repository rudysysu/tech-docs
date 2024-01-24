## OpenVPN（Windows）
- 配置文件地址：C:\Program Files\OpenVPN\config
- 修改配置client.ovpn // 可以改名
```
dev tun // 这里改成tun模式
remote x.y.z  12973 // 这里改成对应的端口
verb 5 // 这里应该是修改日志等级
```

## OpenVPN（Ios）
- 类似Windows，改成tun模式
- 通过iTunes导入配置
- 在OpenVPN上操作导入即可

## XXVPN（Mac）
- 使用移动端的配置，Mac对应的配置用不了
- 直接拖配置到应用上导入即可