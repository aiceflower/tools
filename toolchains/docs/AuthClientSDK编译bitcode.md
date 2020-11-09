### Build Settings

Search Paths设置

```
Framework Search Paths -> $(PROJECT_DIR)/AuthClientSDK/libs
Header Search Paths -> $(PROJECT_DIR)/AuthClientSDK/thirdparty
                       $(PROJECT_DIR)/AuthClientSDK/libs
                       $(PROJECT_DIR)/
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

由于AuthClientSDK是静态库的framework，目前没法针对静态库进行代码混淆；解决办法：可以将AuthClientSDK编译为动态库的framework，或者将静态库编译到app后，对app混淆即可



