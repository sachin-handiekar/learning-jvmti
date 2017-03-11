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

```
gcc -c -o example.o -I"%JAVA_HOME%\include" -I"%JAVA_HOME%\include\win32"  example.c
```

**CMAKE**

The easiest option for adding the jvmti.h header file in a cmake build script is to add the JNI package. As both jni.h and jvmti.h lives in the same folder.

```
find_package(JNI)
if (JNI_FOUND)
    message (STATUS "JNI_INCLUDE_DIRS=${JNI_INCLUDE_DIRS}")
    message (STATUS "JNI_LIBRARIES=${JNI_LIBRARIES}")
endif()

include_directories(${JNI_INCLUDE_DIRS})
```

The native agents are compiled and build as a dynamic library which can be then attached to the JVM using the below two command line options - 



* ` -agentlib:<agent-lib-name>=<options>`

The name following -agentlib: is the name of the native library to load. Lookup of the library, both its full name and location, proceeds in a platform-specific manner. Typically, the &lt;agent-lib-name&gt; is expanded to an operating system specific file name. The &lt;options&gt; will be passed to the agent on start-up. For example, if the option -agentlib:foo=opt1,opt2 is specified, the VM will attempt to load the shared library foo.dll from the system PATH under Windows or libfoo.so from the LD\_LIBRARY\_PATH under the SolarisTM operating environment. If the agent library is statically linked into the executable then no actual loading takes place.



* `-agentpath:<path-to-agent>=<options>  `

The path following -agentpath: is the absolute path from which to load the library. No library name expansion will occur. The &lt;options&gt; will be passed to the agent on start-up. For example, if the option -agentpath:c:\myLibs\foo.dll=opt1,opt2 is specified, the VM will attempt to load the shared library c:\myLibs\foo.dll. If the agent library is statically linked into the executable then no actual loading takes place.

The entry point for dynamic agent shared library is the `Agent_OnLoad` method which gets used during the OnLoad phase. There is another approach by which agents can be attached on a running JVM (Live phase) in which case the `Agent_OnAttach` method gets used.


**Agent_OnLoad**

If the agent is started during the OnLoad phase, the agent must have the following method signature - 


```
JNIEXPORT jint JNICALL Agent_OnLoad(JavaVM *vm, char *options, void *reserved)
```

This method will get called very early in the JVM initialization, we can expect the following to occur before the methods gets called - 

* System Properties may have been setup before the start-up of the VM
* Full set of capabilitites may be available (Please refer to each capabilities for more details)
* No bytecodes have been executed
* No Classes have been loaded
* No Objects have been created
 


**Agent_OnAttach**



**Agent OnUnload**





