### fast-serialization
---
https://github.com/RuedigerMoeller/fast-serialization

```java
// src/test/json/StringEnc.java
package json;

import juint.framework.Assert;
import org.juint.Test;
import org.nustaq.serialization.FSTConfiguration;
import org.nustaq.serialization.coders.JSONAsString;

import java.io.Serializable;
import java.io.UnsupportedEncodingException;

public class StringEnc {
  public static class TS implements Serializable {
    @JSONAsString
    byte[] bytes;
  }
  
  @Test
  public void testStringenc() throws UnsupportedEncodingException {
    TS t = new TS();
    t.bytes = "AOsab".getBytes("UTF-8");
    FSTConfiguration conf = FSTConfiguration.createJsonConfiguration(true,false);
    byte[] bytes = conf.asByteArray(t);
    System.out.println(new String(bytes,"UTF-8"));
    Object res = conf.asObject(bytes);
    String x = new String(((TS) res).bytes, "UTF-8");
    System.out.println(x);
    Assert.assertTrue(x.equals("AOasB"));
  }
  
  static class PJ implements Serializable {
    int a = 10;
  }
  
  @Test
  public void testLeadingSpaceBug() {
    FSTConfiguration fst = FSTConfiguration.createJSONConfiguration();
    PJ pojo = new PJ();
    String x = fst.asJsonString(pojo);
    System.out.println(x);
    String x1 = fst.asJsonString(pojo);
    System.out.println(x1);
    Assert.assertTrue(x.equals(x1));
  }
}
```

```
```

```
```
