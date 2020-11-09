

### Build Settings

Search Paths设置

```
Framework Search Paths -> $(PROJECT_DIR)/../AuthClientSDK/AuthClientSDK/libs
Header Search Paths -> $(PROJECT_DIR)/../AuthClientSDK/AuthClientSDK/libs
                      $(PROJECT_DIR)/../AuthClientSDK/AuthClientSDK/thirdparty
Library Search Paths -> $(PROJECT_DIR)/../AuthClientSDK/AuthClientSDK/libs
```

以下三步为编译bitcode的配置

1） build options设置

```
Enable Bitcode -> No
```

2） Linking 设置

```
Other Linker Flags -> -fembed-bitcode
```

3） Apple Clang - Custom Compiler Flags

```
Other C Falgs -> -fembed-bitcode
```

### 编译

报错找不到bundle，将Build Phrases的Copy Bundle Resourses删掉重新添加即可

```
Showing Recent Messages
/Users/huangjiamin02/Documents/Library/Developer/Xcode/DerivedData/AisinoAuthClient-filjcyakdqowwjdadcyzwwoshprb/Build/Products/Debug-iphoneos/AuthClientBundle.bundle: No such file or directory
```

解决上述问题后还有报错，需要将esand_cloud_ifaa.framework编译为bitcode版本（编译bitcode版本参考以上三步）

```
ld: '/Users/huangjiamin02/Documents/ios/ios-auth-patch-1/AisinoAuthClientSDK/AuthClientSDK/AuthClientSDK/libs/esand_cloud_ifaa.framework/esand_cloud_ifaa(IFAAStatus.o)' does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target. file '/Users/huangjiamin02/Documents/ios/ios-auth-patch-1/AisinoAuthClientSDK/AuthClientSDK/AuthClientSDK/libs/esand_cloud_ifaa.framework/esand_cloud_ifaa' for architecture arm64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

查看动态库或者app是否包含bitcode的方法，__LLVM段的大小许大于1：

```
# otool -l /Users/huangjiamin02/Documents/ios/ios-auth-patch-1/AisinoAuthClientSDK/AuthClientSDK/AuthClientSDK/libs/libAisinoSSL_SM4WB.a | grep LLVM -A 5
...
segname __LLVM
      addr 0x0000000000002d60
      size 0x0000000000000056
    offset 12336
     align 2^4 (16)
    reloff 0
```

