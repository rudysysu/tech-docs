## get() vs getUnchecked()
- 最正统的查询 LoadingCache 的方法是调用 get(k) 方法，这个方法如果查询到已经缓存的值会立即返回，否则使用缓存的 CacheLoader 自动加载一个新值到缓存并返回。因为 CacheLoader 可能会抛出异常，那么如果有异常，则LoadingCache.get(k) 会抛出 ExecutionException 异常。而如果 CacheLoader 抛出 unchecked 未检查的异常，则 get(k) 方法会抛出 UncheckedExecutionException 异常。 
- 此时可以选择使用 getUnchecked(k) 方法，这个方法会将所有的异常包装在 UncheckedExecutionException 异常中。需要注意的是，如果 CacheLoader 声明了检查异常，也就是 CacheLoader 显式的定义了异常，就不能调用 getUnchecked(k) 方法 

## 参数说明
- expireAfterWrite: 指定项在一定时间内没有创建/覆盖时，会移除该key，下次取的时候从loading中取
- expireAfterAccess：指定项在一定时间内没有读写，会移除该key，下次取的时候从loading中取
- refreshAfterWrite：指定时间内没有被创建/覆盖，则指定时间过后，再次访问时，会去刷新该缓存，在新值没有到来之前，始终返回旧值

## example
```java
int userHonorLevel = this.queryUserHonorLevelCache.get(uid);

private LoadingCache<Long, Integer> queryUserHonorLevelCache = CacheBuilder.newBuilder().refreshAfterWrite(5, TimeUnit.SECONDS)
            .build(new CacheLoader<Long, Integer>() {
                @Override
                public Integer load(Long uid) throws Exception {
                    QueryUserHonorRsp queryUserHonorRsp = zhuiwanUserHonorServiceClientFactory.getClient().queryUserHonor(Arrays.asList(uid));
                    if (queryUserHonorRsp.getResult() != 0) {
                        LOG.error("beforeConsume, queryUserHonor, uid: {}, queryUserHonorRsp: {}", uid, queryUserHonorRsp);
                        throw new ServiceException(ServiceErrCode.SERVER_ERR, queryUserHonorRsp.getMsg());
                    }

                    int userHonorLevel = 0;

                    UserGradeSimple userGradeSimple = queryUserHonorRsp.getUserGradeMap().get(uid);
                    if (userGradeSimple != null) {
                        userHonorLevel = userGradeSimple.getLevel();
                    }

                    return userHonorLevel;
                }
            });
```

## 参考文献
- https://einverne.github.io/post/2016/02/google-guava-local-cache-loadingcache.html