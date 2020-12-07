# Table of Contents

- [Table of Contents](#table-of-contents)
- [Getting Started with Simple Web Application](#getting-started-with-simple-web-application)

# Getting Started with Simple Web Application

The following code shows the `build.gradle` file when you choose [`Gradle`](https://gradle.org/).

```gradle
plugins {
    id 'java'
}

group 'io.garam'
version '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    testCompile group: 'junit', name: 'junit', version: '4.12'
    implementation 'io.garam:core:0.4'
}
```

The following code shows the dependencies node of `pom.xml` file when you choose [`Maven`](https://maven.apache.org/).

```xml
<dependency>
  <groupId>io.garam</groupId>
  <artifactId>core</artifactId>
  <version>0.4</version>
  <type>pom</type>
</dependency>
```

Now you can create a controller for a html page, as the following code(`src/main/resources/templates/index.mustache`) shows:  

```mustache
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello Garam Framework!</title>
</head>
<body>
{{ message }}
</body>
</html>
```

Default template engine of Garam is [`Mustache`](https://mustache.github.io/).  

```java
package io.garam;

import io.garam.core.Garam;
import io.garam.core.ui.GaramModel;
import io.garam.core.ui.MustacheTemplateEngine;

import java.util.HashMap;
import java.util.Map;

public class Application {

    public static void main(String[] args) {
        Garam.get("/", ctx -> {
            final Map<String, Object> map = new HashMap<>();
            map.put("message", "Hello Garam!");

            final GaramModel model = new GaramModel(map);
            ctx.render("index", model);
        });

        Garam.port(1234);
        Garam.run();
    }
}
```
