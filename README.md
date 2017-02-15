# Bazel Rules for STM32f4 processors #

* Toolchain: arm-none-eabi-gcc 6.2.1 from [https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads]

## Usage

On `WORKSPACE` add this:

```
git_repository(
    name = "stm32",
    remote = "https://github.com/pedrokiefer/rules_stm32.git",
    commit = "256dd2e75b49485eb4e7844549b5749bb082657a"
    )

load("@stm32//stm32f4:rules.bzl", "arm_none_repository")
arm_none_repository()
``` 
## Available Rules

### arm_none_repository ###

Fetchs arm toolchain

```
load("@stm32//stm32f4:rules.bzl", "arm_none_repository")

arm_none_repository()
```

Run bazel build with `--crosstool_top=@stm32//tools/arm_compiler:toolchain --cpu=armeabi-v7a` for building with this toolchain.

### stm32f4_binary ###

* name: binary_name
* srcs: list of sources
* deps: list of deps
* processor: one of ["STM32F429xx", ... ]
* use_hal: 
* hal_config_hdrs: hal config files generated by stm32cube
* linker_script: linker script to be used

### raw_binary ###
Generates a .bin file
```
raw_binary(
    name = "my_bin",
    src = ":binary"
)
