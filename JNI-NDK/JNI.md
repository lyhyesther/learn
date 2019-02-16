# JNI数据类型
<pre>
/* Primitive types that match up with Java equivalents. */
typedef uint8_t  jboolean; /* unsigned 8 bits */
typedef int8_t   jbyte;    /* signed 8 bits */
typedef uint16_t jchar;    /* unsigned 16 bits */
typedef int16_t  jshort;   /* signed 16 bits */
typedef int32_t  jint;     /* signed 32 bits */
typedef int64_t  jlong;    /* signed 64 bits */
typedef float    jfloat;   /* 32-bit IEEE 754 */
typedef double   jdouble;  /* 64-bit IEEE 754 */

/* "cardinal indices and sizes" */
typedef jint     jsize;
</pre>

# JNI属性

# JNI调用Java层域、方法
<pre>
requirements:
1、访问的方法必须为public
steps:
1、获取Java 类对象
2、获取 方法Id 参数1 Java类对象；参数2 方法名称；参数3 方法签名
3、JNI 调用Java的方法

Java_com_inin_nativego_MainActivity_stringFromJNI(
        JNIEnv *env,
        jobject obj) {
    //1 获取Java 类对象
    jclass _jclaz = env->GetObjectClass(obj);
    //2 获取 方法Id 参数1 Java类对象；参数2 方法名称；参数3 方法签名
    jmethodID _jmethodId = env->GetMethodID(_jclaz, "getStringInJava", "()Ljava/lang/String;");
    jfieldID _jfieldId = env->GetFieldID(_jclaz, "Id", "I");
    //3 JNI 调用Java的方法
    jstring strFromJavaCode = (jstring) env->CallObjectMethod(obj, _jmethodId);
    //获取int 类型的域
    jint id = env->GetIntField(obj, _jfieldId);
    char *chars = (char *) env->GetStringUTFChars(strFromJavaCode, NULL);
    //将int转化为string 类型
    std::string idStr = std::to_string(id);
    char *achars = strcat(chars, idStr.c_str());
//    std::string hello = "Hello from C++";
    return env->NewStringUTF(achars);
}

    //获取域ID
//        env->GetFieldID()
    //获取域
//        env->GetIntField() //获取Int 类型的域
//        env->GetDoubleField()//获取Double类型的域
//        env->GetShortField()//获取Short类型的域
//        env->GetObjectField()//获取对象类型的域
    //获取静态域
//        env->GetStaticFieldID()//获取静态域ID
//        env->GetStaticIntField()//获取静态Int类型的域
//        env->GetStaticObjectField() //获取静态对象类型的域

    //获取方法Id
//        env->GetMethodID()
//        env->CallObjectMethod()//调用对象方法
//        env->CallIntMethod();//调用返回Int类型的方法
//        env->CallObjectMethod()//调用返回对象类型的方法
    //调用静态方法
//        env->CallStaticObjectMethod()调用返回Object类型的静态方法
//        env->CallStaticIntMethod()//调用返回Int类型的静态方法
</pre>


