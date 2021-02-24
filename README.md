## Xposed插件App开发步骤
1. 新建Android项目
2. 将XposedBridge-89.jar包拷贝到/app/libs/目录
3. build.gradle文件`dependencies`中添加`compileOnly fileTree(dir: "libs", include: ["XposedBridge-89.jar"])`
4. 找到/app/src/main下的AndroidManifest.xml 并在application内添加以下内容
```xml
<meta-data
    android:name="xposedmodule"
    android:value="true" />
<meta-data
    android:name="xposeddescription"
    android:value="插件描述文字" />
<!--和XposedBridge-89.jar版本号一致-->
<meta-data
    android:name="xposedminversion"
    android:value="89" />
```
5. /app/src/main/java/包路径/下找到MainActivity, 在同级目录下新建名为Main或者其他名字的Class, 该Class即Hook入口点
6. main下新建folder选择assets, 并在该目录下新建xposed_init文件(txt类型即可)文件写入Hook脚本入口Class, 例如 pkg.MyClassName
7. 实现Class内部逻辑
```java
package com.example.firstandroid;

import de.robv.android.xposed.IXposedHookLoadPackage;
import de.robv.android.xposed.XposedBridge;
import de.robv.android.xposed.callbacks.XC_LoadPackage;

public class XposedInit implements IXposedHookLoadPackage {

    @Override
    public void handleLoadPackage(XC_LoadPackage.LoadPackageParam lpparam) throws Throwable {
        XposedBridge.log("Loaded app: " + lpparam.packageName);
    }
}
```

