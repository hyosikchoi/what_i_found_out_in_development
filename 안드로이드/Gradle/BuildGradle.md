# Android Library MultiModule 작성 시 CommonGradle 설정 방법

* gradle 파일에서 변수를 설정하여 library module인지 application module인지 조건을 통해 설정 값들을 분기 처리한다.

```
def isLibraryPlugin = pluginManager.hasPlugin("com.android.library")
def isApplicationPlugin = pluginManager.hasPlugin("com.android.application")

if (isLibraryPlugin || isApplicationPlugin) {

    android {
        compileSdkVersion compileSdk_Version
        buildToolsVersion buildTools_Version

        defaultConfig {
            if(isApplicationPlugin) {
                applicationId "com.android.application"
            }
            minSdkVersion minSdk_Version
            targetSdkVersion targetSdk_Version
            versionCode versionCode
            versionName versionName

            testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
        }

        dataBinding {
            enabled = true
        }

        buildTypes {
            debug {
                debuggable true

                if (!isLibraryPlugin) {
                    applicationIdSuffix '.dev'
                    resValue "string", "app_name", "clean_Dev"
                }
            }

            release {
                if(isApplicationPlugin){
                    shrinkResources true
                }
                minifyEnabled true
                proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
                if (!isLibraryPlugin) {
                    resValue "string", "app_name", "clean"
                }
            }

            staging {
                initWith debug
                if (!isLibraryPlugin) {
                    applicationIdSuffix '.staging'
                    resValue "string", "app_name", "clean_Staging"
                }
            }
        }

        compileOptions {
            sourceCompatibility JavaVersion.VERSION_1_8
            targetCompatibility JavaVersion.VERSION_1_8
        }

        kotlinOptions {
            jvmTarget = '1.8'
        }

        // Unit Test를 위한 Option
        testOptions {
            unitTests.includeAndroidResources = true
            // return 시 exception 대신에 default Value 를 return 하도록 설정.
            unitTests.returnDefaultValues = true
        }
    }
}
```

* 참고로 **shrinkResources** 값은 Library Module 에서는 설정 안된다.

* 또한 **applicationId** 값도 Application Module 에서만 작성 되어야 한다.

* [MultiModule Gradle 작성 참조](https://github.com/HeeGyeong/ModuleArchitecture/blob/main/CleanArchitectureStudy/android.gradle)



# 오래된 프로젝트 gradle 및 kotlin 버전 마이그레이션 시 유의 사항

* **Cannot choose between the following variants of** 와 같은 에러 메세지가 나올 경우 프로젝트의 **gradle/wrapper/gradle-wrapper.properties file** 에서
```
distributionUrl=https\://services.gradle.org/distributions/gradle-7.4.2-all.zip
```

해당 영역의 gradle 버전을 sync 할 버전으로 바꿔줘야 다운로드를 제대로 받을 수 있다. [stackoverflow 참조](https://stackoverflow.com/questions/73342537/cannot-use-kotlin-1-7-10)