## 常用命令

命令                                                 | 说明
-----------------------------------------------------|-----------------------------------------------------
mvn [options] [<goal(s)>] [<phase(s)>]               | Usage
mvn dependency:sources                               | 下载依赖包源码
mvn clean source:jar install -Dmaven.test.skip=true  | 清除 & 打包源码 & 打包 & 发布 & 忽略单元测试
mvn clean source:jar package -DskipTests             | 清除 & 打包源码 & 打包 & 忽略单元测试
mvn assembly:assembly                                | 打包并装配资源，生成可执行jar
mvn dependency:resolve -Dclassifier=sources          | Download source code
mvn dependency:resolve -Dclassifier=javadoc          | Download javadoc

## 常用参数

参数                        | 说明
----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------
不要忘了clean               | clean能够保证上一次构建的输出不会影响到本次构建。
使用deploy而不是install     | 构建的SNAPSHOT输出应当被自动部署到私有Maven仓库供他人使用，这一点在前面已经详细论述。
使用-U参数                  | 该参数能强制让Maven检查所有SNAPSHOT依赖更新，确保集成基于最新的状态，如果没有该参数，Maven默认以天为单位检查更新，而持续集成的频率应该比这高很多。
使用-e参数                  | 如果构建出现异常，该参数能让Maven打印完整的stack trace，以方便分析错误原因。
使用-Dmaven.repo.local参数  | 如果持续集成服务器有很多任务，每个任务都会使用本地仓库，下载依赖至本地仓库，为了避免这种多线程使用本地仓库可能会引起的冲突，可以使用-Dmaven.repo.local=/home/juven/ci/foo-repo/这样的参数为每个任务分配本地仓库。
使用-B参数                  | 该参数表示让Maven使用批处理模式构建项目，能够避免一些需要人工参与交互而造成的挂起状态。
综上                        | 持续集成服务器上的集成命令应该为 mvn clean deploy -B -e -U -Dmaven.repo.local=xxx 。

## 生命周期

#### Clean Lifecycle

Lifecycle         | Lifecycle phases        | Goal
------------------|-------------------------|--------------------------------------------------------
Clean Lifecycle   | pre-clean               |
--                | clean                   | clean:clean
--                | post-clean              |
Default Lifecycle | validate                |
--                | generate-sources        |
--                | process-sources         | resources:resources
--                | generate-resources      | plugin:descriptor
--                | process-resources       |
--                | compile                 | compiler:compile / compile:compile
--                | process-classes         |
--                | generate-test-sources   | resources:testResources
--                | process-test-sources    |
--                | generate-test-resources |
--                | process-test-resources  |
--                | test-compile            | compiler:testCompile / compile:testCompile
--                | test                    | surefire:test
--                | prepare-package         |
--                | package                 | jar:jar(JAR) / site:attach-descriptor(POM) / war:war(WAR)
--                | pre-integration-test    |
--                | integration-test        |
--                | post-integration-test   |
--                | verify                  |
--                | install                 | install:install
--                | deploy                  | deploy:deploy
Site Lifecycle    | pre-site                |
--                | site                    |
--                | post-site               |
--                | site-deploy             |

