# 同步策略

假设此时有日记因为用户信号不好没有发送出去。

1. 用户再次登录后，调接口 `/diaries` 从服务器拉取其所有日记（因为现在用户的日记还不多，而且每条日记的数据量也不大，可以暂时先这么搞）。
2. 如果某天的日记服务器已经有了，则和本地的比较时间，如果服务器上的比较新，则丢弃本地的。如果本地的比较新，则在界面上显示本地的数据，旁边标记个感叹号。
3. 如果服务器上没有数据，则在界面上显示本地的数据，旁边标记个感叹号。
4. 用户点击感叹号后提示因为网络不好日记没有保存成功，是否重新发送。用户可以选择 `重新发送` 或者 `算了`。