## Sample maven pom files with auth0 dependency

The project attempts to visualise the issue of dependency management using [auth0](https://github.com/auth0/auth0-java) with `okhttp:4.9.0` and quarkus dependencyManagement 
https://github.com/auth0/auth0-java/issues/324

It contains different pom files to visualise the issues managing transitive dependencies

* maven pom file using auth0 [pom.xml](pom.xml)
* maven pom file using auth0 with quarkus dependencyManagement [pom-quarkus-platform.xml](pom-quarkus-platform.xml)
* maven pom file using auth0 with quarkus dependencyManagement [pom-fix.xml](pom-fix.xml)
* maven pom file using auth0 with quarkus dependencyManagement [pom-fix-bom.xml](pom-fix-bom.xml)

### POM Dependencies 

Using [pom.xml](pom.xml) without quarkus the `okhttp` dependencies are `4.9.0`. When using quarkus dependency management [pom-quarkus-platform.xml](pom-quarkus-platform.xml)
the `okhttp` dependencies are downgraded to `3.14.9`.
It can be fixed enforcing dependencies to `4.9.0` like in [pom-fix.xml](pom-fix.xml) or using [bom](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#bill-of-materials-bom-poms) like in [pom-fix-bom.xml](pom-fix-bom.xml)

### Visualise dependencies trees

Run the command to get the different dependencies from the pom files

```shell
mvn -f pom.xml dependency:tree && \
mvn -f pom-quarkus-platform.xml dependency:tree && \
mvn -f pom-fix.xml dependency:tree && \
mvn -f pom-fix-bom.xml dependency:tree
```

```shell
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< org.acme:getting-started >----------------------
[INFO] Building getting-started 1.0.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ getting-started ---
[INFO] org.acme:getting-started:jar:1.0.0-SNAPSHOT
[INFO] \- com.auth0:auth0:jar:1.27.0:compile
[INFO]    +- com.squareup.okhttp3:okhttp:jar:4.9.0:runtime
[INFO]    |  +- com.squareup.okio:okio:jar:2.8.0:runtime
[INFO]    |  |  \- org.jetbrains.kotlin:kotlin-stdlib-common:jar:1.4.0:runtime
[INFO]    |  \- org.jetbrains.kotlin:kotlin-stdlib:jar:1.4.10:runtime
[INFO]    |     \- org.jetbrains:annotations:jar:13.0:runtime
[INFO]    +- com.squareup.okhttp3:logging-interceptor:jar:4.9.0:runtime
[INFO]    |  \- org.jetbrains.kotlin:kotlin-stdlib-jdk8:jar:1.4.10:runtime
[INFO]    |     \- org.jetbrains.kotlin:kotlin-stdlib-jdk7:jar:1.4.10:runtime
[INFO]    +- com.fasterxml.jackson.core:jackson-databind:jar:2.12.1:runtime
[INFO]    |  +- com.fasterxml.jackson.core:jackson-annotations:jar:2.12.1:runtime
[INFO]    |  \- com.fasterxml.jackson.core:jackson-core:jar:2.12.1:runtime
[INFO]    +- commons-codec:commons-codec:jar:1.15:runtime
[INFO]    \- com.auth0:java-jwt:jar:3.12.1:runtime
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.774 s
[INFO] Finished at: 2021-03-12T10:52:32+01:00
[INFO] ------------------------------------------------------------------------
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< org.acme:getting-started >----------------------
[INFO] Building getting-started 1.0.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ getting-started ---
[INFO] org.acme:getting-started:jar:1.0.0-SNAPSHOT
[INFO] \- com.auth0:auth0:jar:1.27.0:compile
[INFO]    +- com.squareup.okhttp3:okhttp:jar:3.14.9:runtime
[INFO]    |  \- com.squareup.okio:okio:jar:1.17.2:runtime
[INFO]    +- com.squareup.okhttp3:logging-interceptor:jar:3.14.9:runtime
[INFO]    +- com.fasterxml.jackson.core:jackson-databind:jar:2.12.1:runtime
[INFO]    |  +- com.fasterxml.jackson.core:jackson-annotations:jar:2.12.1:runtime
[INFO]    |  \- com.fasterxml.jackson.core:jackson-core:jar:2.12.1:runtime
[INFO]    +- commons-codec:commons-codec:jar:1.14:runtime
[INFO]    \- com.auth0:java-jwt:jar:3.12.1:runtime
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.899 s
[INFO] Finished at: 2021-03-12T10:52:34+01:00
[INFO] ------------------------------------------------------------------------
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< org.acme:getting-started >----------------------
[INFO] Building getting-started 1.0.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ getting-started ---
[INFO] org.acme:getting-started:jar:1.0.0-SNAPSHOT
[INFO] \- com.auth0:auth0:jar:1.27.0:compile
[INFO]    +- com.squareup.okhttp3:okhttp:jar:4.9.0:runtime
[INFO]    |  +- com.squareup.okio:okio:jar:2.8.0:runtime
[INFO]    |  |  \- org.jetbrains.kotlin:kotlin-stdlib-common:jar:1.4.20:runtime
[INFO]    |  \- org.jetbrains.kotlin:kotlin-stdlib:jar:1.4.20:runtime
[INFO]    |     \- org.jetbrains:annotations:jar:13.0:runtime
[INFO]    +- com.squareup.okhttp3:logging-interceptor:jar:4.9.0:runtime
[INFO]    |  \- org.jetbrains.kotlin:kotlin-stdlib-jdk8:jar:1.4.20:runtime
[INFO]    |     \- org.jetbrains.kotlin:kotlin-stdlib-jdk7:jar:1.4.20:runtime
[INFO]    +- com.fasterxml.jackson.core:jackson-databind:jar:2.12.1:runtime
[INFO]    |  +- com.fasterxml.jackson.core:jackson-annotations:jar:2.12.1:runtime
[INFO]    |  \- com.fasterxml.jackson.core:jackson-core:jar:2.12.1:runtime
[INFO]    +- commons-codec:commons-codec:jar:1.14:runtime
[INFO]    \- com.auth0:java-jwt:jar:3.12.1:runtime
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.819 s
[INFO] Finished at: 2021-03-12T10:52:36+01:00
[INFO] ------------------------------------------------------------------------
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< org.acme:getting-started >----------------------
[INFO] Building getting-started 1.0.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ getting-started ---
[INFO] org.acme:getting-started:jar:1.0.0-SNAPSHOT
[INFO] \- com.auth0:auth0:jar:1.27.0:compile
[INFO]    +- com.squareup.okhttp3:okhttp:jar:4.9.0:runtime
[INFO]    |  +- com.squareup.okio:okio:jar:2.8.0:runtime
[INFO]    |  |  \- org.jetbrains.kotlin:kotlin-stdlib-common:jar:1.4.20:runtime
[INFO]    |  \- org.jetbrains.kotlin:kotlin-stdlib:jar:1.4.20:runtime
[INFO]    |     \- org.jetbrains:annotations:jar:13.0:runtime
[INFO]    +- com.squareup.okhttp3:logging-interceptor:jar:4.9.0:runtime
[INFO]    |  \- org.jetbrains.kotlin:kotlin-stdlib-jdk8:jar:1.4.20:runtime
[INFO]    |     \- org.jetbrains.kotlin:kotlin-stdlib-jdk7:jar:1.4.20:runtime
[INFO]    +- com.fasterxml.jackson.core:jackson-databind:jar:2.12.1:runtime
[INFO]    |  +- com.fasterxml.jackson.core:jackson-annotations:jar:2.12.1:runtime
[INFO]    |  \- com.fasterxml.jackson.core:jackson-core:jar:2.12.1:runtime
[INFO]    +- commons-codec:commons-codec:jar:1.14:runtime
[INFO]    \- com.auth0:java-jwt:jar:3.12.1:runtime
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.820 s
[INFO] Finished at: 2021-03-12T10:52:38+01:00
[INFO] ------------------------------------------------------------------------
```