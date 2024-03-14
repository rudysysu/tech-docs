其实就是事务的拦截器，可以切入事务做一些事情，比如：

TransactionSynchronizationManager.registerSynchronization(new TransactionSynchronization() {
    @Override
    public void beforeCommit(boolean readOnly) {
        log.info("事务开始提交");
    }

    @Override
    public void afterCommit() {
        log.info("事务提交结束");
    }
});