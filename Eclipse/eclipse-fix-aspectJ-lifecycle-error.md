<build>
  <pluginManagement>
    <!-- Fix AspectJ lifecycle error in eclipes -->
    <plugins>
      <plugin>
        <groupId>org.eclipse.m2e</groupId>
        <artifactId>lifecycle-mapping</artifactId>
        <version>1.0.0</version>
        <configuration>
          <lifecycleMappingMetadata>
            <pluginExecutions>
              <pluginExecution>
                <pluginExecutionFilter>
                  <groupId>org.codehaus.mojo</groupId>
                  <artifactId>aspectj-maven-plugin</artifactId>
                  <versionRange>[1.0,)</versionRange>
                  <goals>
                    <goal>test-compile</goal>
                    <goal>compile</goal>
                  </goals>
                </pluginExecutionFilter>
                <action>
                  <execute />
                </action>
              </pluginExecution>
            </pluginExecutions>
          </lifecycleMappingMetadata>
        </configuration>
      </plugin>
    </plugins>
  </pluginManagement>
 
  <!-- Other config -->
<build>






问题：
Plugin execution not covered by lifecycle configuration: org.codehaus.groovy:groovy-eclipse-compiler:2.9.1-01:add-groovy-build-paths (execution: default-add-groovy-build-paths, phase: initialize)

解决：
Window-Perferences-Maven-Lifecycle Mapping
点击Open workspace lifecycle mappings metadata。加入如下内容：
C:/Users/eyogdig/data/workspaces-eric/.metadata/.plugins/org.eclipse.m2e.core/lifecycle-mapping-metadata.xml
<lifecycleMappingMetadata>
    <pluginExecutions>
        <pluginExecution>
            <pluginExecutionFilter>
                <groupId>org.codehaus.groovy</groupId>
                <artifactId>groovy-eclipse-compiler</artifactId>
                <versionRange>[2.9.1-01,)</versionRange>
                <goals>
                    <goal>add-groovy-build-paths</goal>
                </goals>
            </pluginExecutionFilter>
            <action>
                <ignore />
            </action>
        </pluginExecution>
    </pluginExecutions>
</lifecycleMappingMetadata>

参考文献：
https://blog.csdn.net/bedpotato/article/details/18350247
