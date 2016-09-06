---
layout: page
title: Development 
permalink: /development/
navi: 4
---

Release a new Pustefix version
==============================

The Pustefix Framework is available on [Maven Central](https://repo1.maven.org/maven2/org/pustefixframework/). New releases are published to this repository using
the free [Sonatype service](http://central.sonatype.org/).

For deploying a release or snapshot, you will have to configure the according server and your credentials in the Maven settings. Additionally you have to set the
GPG passphrase for signing the artifacts:

{% highlight xml %}
<settings>
  <servers>
    <server>
      <id>pustefix</id>
      <username>pustefix</username>
    </server>
    <server>
      <id>sonatype-nexus-snapshots</id>
      <username>SONATYPE_USER</username>
      <password>SONATYPE_PASSWORD</password>
    </server>
    <server>
      <id>sonatype-nexus-staging</id>
      <username>SONATYPE_USER</username>
      <password>SONATYPE_PASSWORD</password>
    </server>
  </servers>
  <profiles>
    <profile>
      <id>release-properties</id>
      <activation>
        <property>
          <name>performRelease</name>
          <value>true</value>
        </property>
      </activation>
      <properties>                                                   
        <gpg.passphrase>GPG_PASSPHRASE</gpg.passphrase>
      </properties>
    </profile>
  </profiles>
</settings>
{% endhighlight %}

Having set up Maven, you can just checkout Pustefix and use the Maven release plugin to build and deploy it:

{% highlight text %}
$ git clone https://github.com/pustefix-projects/pustefix-framework.git release
$ cd release
$ mvn -B release:prepare
$ mvn release:perform
{% endhighlight %}

Pustefix will be deployed to the Sonatype staging repository. To make it available on Maven Central you have
to close and release it using the [Sonatype web interface](https://oss.sonatype.org/index.html#stagingRepositories).


