## ��������

����                                                 | ˵��
-----------------------------------------------------|-----------------------------------------------------
mvn [options] [<goal(s)>] [<phase(s)>]               | Usage
mvn dependency:sources                               | ����������Դ��
mvn clean source:jar install -Dmaven.test.skip=true  | ��� & ���Դ�� & ��� & ���� & ���Ե�Ԫ����
mvn clean source:jar package -DskipTests             | ��� & ���Դ�� & ��� & ���Ե�Ԫ����
mvn assembly:assembly                                | �����װ����Դ�����ɿ�ִ��jar
mvn dependency:resolve -Dclassifier=sources          | Download source code
mvn dependency:resolve -Dclassifier=javadoc          | Download javadoc

## ���ò���

����                        | ˵��
----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------
��Ҫ����clean               | clean�ܹ���֤��һ�ι������������Ӱ�쵽���ι�����
ʹ��deploy������install     | ������SNAPSHOT���Ӧ�����Զ�����˽��Maven�ֿ⹩����ʹ�ã���һ����ǰ���Ѿ���ϸ������
ʹ��-U����                  | �ò�����ǿ����Maven�������SNAPSHOT�������£�ȷ�����ɻ������µ�״̬�����û�иò�����MavenĬ������Ϊ��λ�����£����������ɵ�Ƶ��Ӧ�ñ���ߺܶࡣ
ʹ��-e����                  | ������������쳣���ò�������Maven��ӡ������stack trace���Է����������ԭ��
ʹ��-Dmaven.repo.local����  | ����������ɷ������кܶ�����ÿ�����񶼻�ʹ�ñ��زֿ⣬�������������زֿ⣬Ϊ�˱������ֶ��߳�ʹ�ñ��زֿ���ܻ�����ĳ�ͻ������ʹ��-Dmaven.repo.local=/home/juven/ci/foo-repo/�����Ĳ���Ϊÿ��������䱾�زֿ⡣
ʹ��-B����                  | �ò�����ʾ��Mavenʹ��������ģʽ������Ŀ���ܹ�����һЩ��Ҫ�˹����뽻������ɵĹ���״̬��
����                        | �������ɷ������ϵļ�������Ӧ��Ϊ mvn clean deploy -B -e -U -Dmaven.repo.local=xxx ��

## ��������

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

