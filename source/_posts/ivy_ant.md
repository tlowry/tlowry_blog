---
title: Adding Apache ivy to an Ant build.xml without ivy.xml
---
* No ivy.xml required
* Assumes ivy jar is at /my_jar_dir/ivy-2.5.0.jar

1. add xml namespace for ivy to project element to prevent task name clashes:

```xml
    xmlns:ivy="antlib:org.apache.ivy.ant

    <project xmlns:ivy="antlib:org.apache.ivy.ant" name="My Java App" default="compile">
```

2. define the ivy tasks and point to the jar where they are stored:
```xml
<taskdef  uri="antlib:org.apache.ivy.ant" classpath="/my_jar_dir/ivy-2.5.0.jar"/>
```

3. Download dependencies into lib directory (inside prep task)
```xml
    <!-- Pull jars from maven, javadoc + sources go in sub dirs -->
    <ivy:retrieve pattern="lib/([classifier])/[artifact]-[revision](-[classifier]).[ext]">

<dependency org="org.apache.httpcomponents" name="httpclient" rev="4.5.11" conf="default,javadoc,sources"/>
    <dependency org="org.jruby" name="jruby-complete" rev="9.2.9.0" conf="default,javadoc,sources"/>
    </ivy:retrieve>

    <!-- Replace existing project.class.path if set -->
    <path id="project.class.path">
    <fileset dir="lib" includes="*.jar"/>
    </path>

    <pathconvert property="newPath" refid="project.class.path" />
    <echo> NEW CLASSPATH is ${newPath}</echo>
```
