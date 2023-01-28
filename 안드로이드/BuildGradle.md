# Android Library MultiModule 작성 시 Flavor 및 BuildType 설정 방법

* 원래 App 모듈의 Flavor 와 BuildType 을 맞춰줘야 한다.

* App 모듈 gradle 에서 Flavor 및 BuildType 설정

```
// Custom Build Variant
    flavorDimensions "app"
    productFlavors {fitpet {}}
    apply from: project.file('build-develop.gradle')
    apply from: project.file('build-staging.gradle')
    apply from: project.file('build-product.gradle')
    apply from: project.file('build-release.gradle')
    android.variantFilter { variant ->
        variant.setIgnore(variant.buildType.name == 'debug')
    }
```

* app 모듈에는 file 형태로 buildType 이 develop , staging , product , release 가 구성되어 있다.


* Android Library Module gradle 에서 Flavor 및 BuildType 설정

```
 // Custom Build Variant
    flavorDimensions "app"
    productFlavors {fitpet {}}
    android.variantFilter { variant ->
        variant.setIgnore(variant.buildType.name == 'debug')
    }

    buildTypes {
        develop {}
        staging {}
        product {}
        release {}
    }
```

* 해당 설정을 맞춰주게 되면 App 모듈의 Variant를 develop 으로 하게 되면 Library 모듈도 따라서 develop 으로 자동 설정 되게 된다. 