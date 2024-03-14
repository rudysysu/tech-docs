1. 创建临时表
2. 修改临时表模型
3. 拷贝数据到临时表
4. 删除旧表
5. 重命名临时表
6. 然后在原表上加三个触发器，DELETE/UPDATE/INSERT，将原表中要执行的语句也在新表中执行
7. 直接用工具：pt-online-schema-change
8. 参见：https://cloud.tencent.com/developer/article/1524019