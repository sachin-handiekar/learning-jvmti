# JNI Crash Course

This chapter we'll cover the basics of using the Java Native Interface.which will be very useful in developing JVMTI Agents.

### Data Types

| **Java**  | **Native** | **Description** |
| :--- | :--- | :--- |
| boolean | jboolean | unsigned 8 bits |
| byte | jbyte | signed 8 bits |
| char | jchar | unsigned 16 bits |
| short | jshort | signed 16 bits |
| int | jint | signed 32 bits |
| long | jlong | signed 64 bits |
| float | jfloat | 32 bits |
| double | jdouble | 64 bits |
| void | void | N/A |

### 

### Type Signatures

| **Type Signature** | **Java Type** |
| :--- | :--- |
| Z | boolean |
| B | byte |
| C | char |
| S | short |
| I | int |
| J | long |
| F | float |
| D | double |
| L fully-qualified-class ; | fully-qualified-class |
| \[ type | type\[\] |
| \( arg-types \) ret-type | method type |

For example, the Java method:

```
long f (int n, String s, int[] arr);
```

has the following type signature:

```
(ILjava/lang/String;[I)J
```

> **Hint :**
>
> Use javap to generate method signature.



