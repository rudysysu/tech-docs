## 方案1
- 创建不同的topic，代表不同的延迟时间
- 通过sleep实现延迟。这里注意不要sleep太久，要不会触发再平衡

## 方案2
- 创建不同的topic，代表不同的延迟时间
- 通过Consumer的pause，resume实现延迟。这里注意不要sleep太久，要不会触发再平衡
- 通过seek修改分区的offset

## 参考
- https://zhuanlan.zhihu.com/p/365802989
- https://www.infoq.cn/article/2ymoli5o2ooj1vw3r3q7