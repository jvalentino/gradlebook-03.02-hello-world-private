## 3.2 Dealing with a non-public Gradle Distribution

At most companies, your development environments and related tools are not able to connect directly to the public internet. Your company network requires you to go through a Proxy in order to access to outside internet. While your web browsers are setup to be able to use this Corporate Proxy, which is why you sometimes get prompted for your employee ID and password, your command-line, specifically Gradle, is not.

In a development infrastructure in which you are not directly connecting to the outside internet, it is also highly likely that you are running your own development tools within your corporate network, specifically centralized dependency management. Whether Artifactory (https://jfrog.com/artifactory), Nexus (https://www.sonatype.com/nexus-repository-sonatype), or something else, your dependencies are centralized at a location that is not on the public internet. For the purpose of the Gradle Wrapper, this means that the **gradle-wrapper.properties** file will have to be modified to reference that location.

For example:

```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=http://localhost:8081/artifactory/gradle-release-local/gradle-4.3-bin.zip
```

The **distributionUrl** is what is expected to point to a zip file that contains the appropriate Gradle distribution. In the above example it was modified to point to the location on an Artifactory server that is running locally (as evident by **localhost**). If you intend to run using the Gradle Wrapper on a corporate network, you will need to ensure **distributionUrl** points to a working location.

