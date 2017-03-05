# JVMTI Examples

A collection of working JVMTI Examples - 

## Hello JVMTI Agent

In this first example, we will see how we can easily build a native agent using the JVMTI API -

1. Let's create a simple C file with the below code - 

```cpp
#include <jvmti.h>
#include <stdio.h>

JNIEXPORT jint JNICALL Agent_OnLoad(JavaVM *jvm, char *options, void *reserved) {
    printf("I'm a native Agent....");
    return JNI_OK;
}
```

1. Now let's compile the code using gcc and build a library - 

```bash
gcc -c -o simpleJVMTI.o -I"%JAVA_HOME%\include" -I"%JAVA_HOME%\include\win32"  SimpleJVMTI.c
```

On Windows, we will create a DLL file -

```bash
gcc -shared -o simpleJVMTI.dll  simpleJVMTI.o
```

1. After building our Agent library, now let's create a simple Java application -

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("I'm inside main()");
    }
}
```

1. Now let's run our Java Application with our JVMTI Agent - 

```bash
java -agentpath:C:/path/to/simpleJVMTI.dll HelloWorld
```

Output :

```bash
I'm inside main()
I'm a native Agent....
```





