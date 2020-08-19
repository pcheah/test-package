# test-package

Generic instructions. Copy and customize for packages that we publish to Github Packages.

## Getting Started

1. [Set up a personal access token](https://docs.github.com/en/packages/publishing-and-managing-packages/about-github-packages#about-tokens) for use with Github Packages. I recommend adding all the scopes they mention (repo, read:packages, write:packages, delete:packages) to cover most use cases during development.
2. [Add the token to your ~/.m2/settings.xml file](https://docs.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-apache-maven-for-use-with-github-packages)

Example ``~/.m2/settings.xml`` file:

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>github</id>
      <username>USERNAME</username>
      <password>TOKEN</password>
    </server>
  </servers>
</settings>
```

Replace USERNAME with your Github user name. Replace TOKEN with the personal access token you set up for Github Packages.

## Publishing a package to Github Packages

In the package project's ``pom.xml`` file, add a distribution management section:

```xml
    <distributionManagement>
        <repository>
            <id>github</id>
            <name>test-package on Github Packages</name>
            <url>https://maven.pkg.github.com/pcheah/test-package</url>
        </repository>
    </distributionManagement>
```

There is a default publishing location if you do not have a distribution management section but if we plan to publish multiple packages to the same repository, we do need this section.

Then publish the package to Github Packages using Maven:

```sh
$ mvn deploy
```

## Using this package in a Maven project

Add this repository to the repositories section in pom.xml:

```xml
    <repositories>
        <repository>
            <id>github</id>
            <name>test-package on GitHub Packages</name>
            <url>https://maven.pkg.github.com/pcheah/test-package</url>
        </repository>
    </repositories>
```

Then add this dependency to the dependencies section in pom.xml:

```xml
    <dependencies>
        <dependency>
            <groupId>com.icetec</groupId>
            <artifactId>test-package</artifactId>
            <version>0.1</version>
        </dependency>
    </dependencies>
```

## References

* [GitHub Packages](https://docs.github.com/en/packages)
* [About GitHub Packages](https://docs.github.com/en/packages/publishing-and-managing-packages/about-github-packages)
* [Configuring Apache Maven for use with GitHub Packages](https://docs.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-apache-maven-for-use-with-github-packages)
