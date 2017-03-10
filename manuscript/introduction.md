# Introduction

## What is JVM Tool Interface \(JVMTI\)?

The JVMTool Interface \(JVMTI\) is an API used for creating development and monitoring tools. It provides us with a way to inspect the state and to control the execution on an application in the JVM.

JVMTI is a two-way interface it provides the agent \(the client of JVMTI API\) with notification of important event occurrences. And we can also query and control the application throught the various functions provided by the API.

Native agents run in the same process and communicate directly with the JVM they are being executed. The native in-process interface allows maximal control with minimal intrusion on the part of a tool.

## Developing Native Agents using JVMTI API

JVMTI Agents can be develop in any native language which supports C language calling conventions

The function, event, data type, and constant definitions needed for using JVMTI are defined in the include file `jvmti.h`, which can be found in the `%JAVA_HOME%/include` directory. To use this include file add the JDK Include directory path to the include path and add the following line to the source code –

`#include <jvmti.h>`

Below are some examples showing the usage of include path in the build script -

**Make**

GCC



G++



**CMAKE**

The easiest option for adding the jvmti.h header file in a cmake build script is to add the JNI package. As both jni.h and jvmti.h lives in the same folder. 

```
find_package(JNI)
if (JNI_FOUND)
    message (STATUS "JNI_INCLUDE_DIRS=${JNI_INCLUDE_DIRS}")
    message (STATUS "JNI_LIBRARIES=${JNI_LIBRARIES}")
endif()
```









