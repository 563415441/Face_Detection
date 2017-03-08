
[toc]

---

#<center>**AS ���� OpenCV ����֮ face-detection**</center>

---

#***TODO***

- [] 

---

#***Reference***

* [AndroidStudio2.2��opencv���������](http://blog.csdn.net/ddjjll8877/article/details/52669593 "http://blog.csdn.net/ddjjll8877/article/details/52669593")

* [AS2.2ʹ��CMake��ʽ����JNI/NDK����](http://www.jianshu.com/p/cb3064450688 "http://www.jianshu.com/p/cb3064450688")

* [AndroidStudio2.2������CMake���뷽ʽ��NDK opencv����](http://blog.csdn.net/ddjjll8877/article/details/52670097 "http://blog.csdn.net/ddjjll8877/article/details/52670097")

* [Android Studio 2.2 NDK���� opencv ����ʶ��](http://blog.csdn.net/a992036795/article/details/53200353 "http://blog.csdn.net/a992036795/article/details/53200353")

---

#**׼������**

���� [��Eclipse ���� OpenCV ����֮ face-detection��]( "")��

---

#**���빤��**

##**�� AS �������¹���**

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/01.png)

##**�� Android ��ͼתΪ Project ��ͼ**

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/02.png)

##**��� NDK ֧��**

>File -> Project Structure...

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/03.png)

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/04.png)

##**���� lib ģ��**

>File -> New -> Import Module...

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/05.png)

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/06.png)

###**���������**

####**target δ�ҵ�**

#####**Question**

> Error:Failed to find target with hash string 'android-*' in: *

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/07.png)

#####**Why**

δ��װ Android 14 �� SDK��

#####**Answer**

�����Ѱ�װ�İ汾��

Դ���룺

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/08.png)

�޸�Ϊ��

    apply plugin: 'com.android.library'
    
    android {
        compileSdkVersion 25
        buildToolsVersion "25.0.2"
    
        defaultConfig {
            minSdkVersion 18
            targetSdkVersion 25
        }
    
        buildTypes {
            release {
                minifyEnabled false
                proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.txt'
            }
        }
    }

���±��롣

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/09.png)

##**��� app ģ��� lib ģ�������**

>File -> Project Structure...

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/10.png)

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/11.png)

ѡ�� lib��

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/12.png)

##**��� app ģ��� JNI lib**

###**�½� jniLibs Ŀ¼**

>�Ҽ� main -> New -> Directory

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/13.png)

###**���� JNI lib �ļ��� jniLibs**

JNI lib �ļ�����Ŀ¼��D:\OpenCV-3.2.0-android-sdk\sdk\native\libs

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/14.png)

###**���� JNI lib**

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/15.png)

�޸ĺ󣬴���Ϊ��

    apply plugin: 'com.android.application'
    
    android {
        compileSdkVersion 25
        buildToolsVersion "25.0.2"
        defaultConfig {
            applicationId "io.weichao.face_detection"
            minSdkVersion 18
            targetSdkVersion 25
            versionCode 1
            versionName "1.0"
            testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
            externalNativeBuild {
                cmake {
                    cppFlags "-std=c++11 -frtti -fexceptions"
                    abiFilters 'x86', 'x86_64', 'armeabi', 'armeabi-v7a', 'arm64-v8a', 'mips', 'mips64'
                }
            }
        }
        buildTypes {
            release {
                minifyEnabled false
                proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
            }
        }
        externalNativeBuild {
            cmake {
                path "CMakeLists.txt"
            }
        }
        sourceSets {
            main {
                jniLibs.srcDirs = ['D:\\android_studio_workspace\\Face_Detection\\app\\src\\main\\jniLibs']
            }
        }
    }
    
    dependencies {
        compile fileTree(include: ['*.jar'], dir: 'libs')
        androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
            exclude group: 'com.android.support', module: 'support-annotations'
        })
        compile 'com.android.support:appcompat-v7:25.2.0'
        compile 'com.android.support.constraint:constraint-layout:1.0.1'
        testCompile 'junit:junit:4.12'
        compile project(':openCVLibrary320')
    }

###**���±���**

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/16.png)

##**���� face-detection ���̵���Դ�ļ��� app ģ��**

��Դ�ļ�����Ŀ¼��D:\OpenCV-3.2.0-android-sdk\samples\face-detection\res

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/17.png)

##**ɾ�� app ģ�� java �ļ������� face-detection ���̵�Դ�����ļ��� app ģ��**

Դ�����ļ�����Ŀ¼��D:\OpenCV-3.2.0-android-sdk\samples\face-detection\src

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/18.png)

##**�滻 AndroidManifest.xml**

AndroidManifest.xml �ļ�·����D:\OpenCV-3.2.0-android-sdk\samples\face-detection\AndroidManifest.xml

##**ɾ�� app ģ�� C/C++ �ļ������� face-detection ���̵� C/C++ �ļ��� app ģ��**

C/C++ �ļ�����Ŀ¼��D:\OpenCV-3.2.0-android-sdk\samples\face-detection\jni

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/19.png)

##**�޸� CMakeLists.txt**

    #CMake�汾��Ϣ
    cmake_minimum_required(VERSION 3.4.1)
    
    # ֧��-std=gnu++11
    set(CMAKE_VERBOSE_MAKEFILE on)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")
    
    # ����·��
    set(pathToProject D:/android_studio_workspace/Face_Detection)
    # OpenCV-android-sdk·��
    set(pathToOpenCv D:/OpenCV-3.2.0-android-sdk)
    
    # ���ü���native����
    include_directories(${pathToOpenCv}/sdk/native/jni/include)
    
    # ��Ӵ������cpp�ļ�
    add_library(DetectionBasedTracker_jni SHARED ${pathToProject}/app/src/main/cpp/DetectionBasedTracker_jni.h ${pathToProject}/app/src/main/cpp/DetectionBasedTracker_jni.cpp)
    
    # ��̬��ʽ����
    add_library(lib_opencv SHARED IMPORTED)
    # ����libopencv_java3.so�ļ�
    set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${pathToProject}/app/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so)
    
    target_link_libraries(DetectionBasedTracker_jni lib_opencv log)

###**���������**

####**�޷�ʹ�õ���İ�**

#####**Question**

>Unused import statement

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/20.png)

#####**Why**

* [C������<>�͡�����ʲô����](https://zhidao.baidu.com/question/488136758.html "https://zhidao.baidu.com/question/488136758.html")

`<>`����ϵͳĬ�ϵ�Ŀ¼����ͷ�ļ���`""`���ں���ĵ�ǰ�����ļ���ͬ��Ŀ¼����ͷ�ļ���Դ���벻�Ͻ������Դ˴��Ҳ����ļ���

#####**Question**

�޸Ĵ���`#include <DetectionBasedTracker_jni.h>`Ϊ`#include "DetectionBasedTracker_jni.h"`

####**����δ����**

#####**Question**

>undefined reference to `__android_log_print'

![](http://github.com/weichao66666/Face_Detection/raw/master/README.md-images/21.png)

#####**Why**

* [undefined reference to `__android_log_print'](http://stackoverflow.com/questions/4455941/undefined-reference-to-android-log-print "http://stackoverflow.com/questions/4455941/undefined-reference-to-android-log-print")

OpenCV SDK �е� liblog.so δ���롣

#####**Answer**

    target_link_libraries(log)

---

#**����**

���гɹ���

�������[��Eclipse ���� OpenCV ����֮ face-detection��]( "")һ�£�

---









