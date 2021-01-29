1. android/.gitignore　の設定
2. build.gradle
 - 2.1 总体图
```xml
  apply plugin: 'com.android.application'

android {
    compileSdkVersion 24
    buildToulsVersion "25.0.2"
    /**
     * 一、默认产品偏好配置
     */
    defaultConfig {
        ...
    }
    /**
     * 二、自定义签名配置
     */
    signingConfigs {
        config {
          ...
        }
    }
    /**
     * 三、构建类型，分为release和debug两种
     */
    buildTypes {
        release {
          ...
        }
        debug {
          ...
        }
    }
    /**
     * 四、自定义产品偏好配置，可以定义多个偏好产品
     */
    productFlavors {
        demo {
            applicationId "cn.teahcourse.demo"
            versionName "1.0-demo"
            signingConfig signingConfigs.config
        }
        personal{
          ...
        }
        enterprise{
          ...
        }
    }
    /**
     *五、DEX文件构建属性配置（加快构建速度）
     */
    dexOptions {
        ...
    }
    /**
     * 六、将一个apk拆分成多个相关配置（拆分依据：屏幕密度、系统架构）
     */
    splits {
        density {
           ...
        }
        abi {
           ...
        }
    }
}
/**
 * 七、引入依赖包的秘密
 */
dependencies {
   ...
}
```

  - 2.2 
```xml
对于 productFlavors 块中的每个变种，您可以重新定义 applicationId 属性，也可以使用 applicationIdSuffix 在默认的应用 ID 上追加一段，如下所示：

   android {
    defaultConfig {
        applicationId "com.example.myapp"
    }
    productFlavors {
        free {
            applicationIdSuffix ".free"
        }
        pro {
            applicationIdSuffix ".pro"
        }
    }
   }
```
 - 2.3 配置安全的自定义签名
 可以使用语法 keystoreProperties[‘属性名称’] 引用存储在 	 keystoreProperties 中的属性。修改模块 build.gradle 文件的 signingConfigs 块，以便使用此语法引用存储在 keystoreProperties 中的签署信息。
```xml
  android {
 		signingConfigs {
     		config {
         		keyAlias keystoreProperties['keyAlias']
         		keyPassword keystoreProperties['keyPassword']
         		storeFile file(keystoreProperties['storeFile'])
         		storePassword keystoreProperties['storePassword']
     			}
 		}

   
```
 - 2.4 构建类型
 每一个APP至少包含 debug 和 release 两种构建类型， debug 定义APP的调试版本， debug 模式的几个特点：
  -- 支持断点调试和log信息打印， debuggable 属性值为 true
  -- 使用系统默认的密钥库签署apk文件
  -- 没有对apk文件进行代码和资源文件的优化（包括文件压缩、冗余文件删除）
  -- 没有对代码进行混淆
	
 - 2.5 productFlavors
	[productFlavors](https://www.jianshu.com/p/7c0e14b9b286)
	
 - 2.6 resvalue
	[解释resvalue](https://blog.csdn.net/xx326664162/article/details/49247815)

 - 2.7 String.xml
 [从String.xml里面取值来替换app_name](https://blog.csdn.net/jerycoupter/article/details/70159410)
 ```xml
 修改 res value 的方式，比如修改 strings.xml 文件中的 AppName 的值

在你的 gradle 文件 buildTypes 或者 productFlavors 下面，如 release 体内写上类似：
resValue "string", "AppName", "app1"
相当于在res/strings.xml 下增加一个名为 AppName，值为app1 的资源。在java中的使用resValue和strings.xml的方法是一样的，
```
 - 2.8 纏め
	[总结productFlavors](https://blog.csdn.net/xx326664162/article/details/48467343)
	