## 依赖

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-text</artifactId>
    <version>1.9</version> <!-- 或者使用最新版本 -->
</dependency>
```

## 使用

```java
package com.xxgcx.controller.user;

import org.apache.commons.text.StringEscapeUtils;

public class Main {
    public static void main(String[] args) {
        // 将标签转义
        String escapedHtml = StringEscapeUtils.escapeHtml4("<a>1222</a>");
        // 将转义字符恢复
        String unescapeHtml4 = StringEscapeUtils.unescapeHtml4(escapedHtml);
        System.out.println(unescapeHtml4);
    }
}
```