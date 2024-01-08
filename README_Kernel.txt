################################################################################
1. How to Build
        - get Toolchain
                get the proper toolchain packages from AOSP or CodeSourcery or ETC.
                (Download link : https://opensource.samsung.com/uploadSearch?searchValue=toolchain )
                Please decompress in 'kernel_platform' folder
                (toolchain path : kernel_platform\prebuilts)

        - Set and export target config
                1. target config
                        BUILD_TARGET=dm3q_eur_openx
                        export MODEL=$(echo ${BUILD_TARGET} | cut -d'_' -f1)
                        export PROJECT_NAME=${MODEL}
                        export REGION=$(echo ${BUILD_TARGET} | cut -d'_' -f2)
                        export CARRIER=$(echo ${BUILD_TARGET} | cut -d'_' -f3)
                        export TARGET_BUILD_VARIANT= user
                        
                2. Chipset common config
                        CHIPSET_NAME=kalama
                        export ANDROID_BUILD_TOP=$(pwd)
                        export TARGET_PRODUCT=gki
                        export TARGET_BOARD_PLATFORM=gki

                        export ANDROID_PRODUCT_OUT=${ANDROID_BUILD_TOP}/out/target/product/${MODEL}
                        export OUT_DIR=${ANDROID_BUILD_TOP}/out/msm-kernel-${CHIPSET_NAME}-${TARGET_PRODUCT}

                        # for Lcd(techpack) driver build
                        export KBUILD_EXTRA_SYMBOLS="/home/dpi/qb5_8814/workspace/P4_1716/android/out/vendor/qcom/opensource/mmrm-driver/Module.symvers                                                                         /home/dpi/qb5_8814/workspace/P4_1716/android/out/vendor/qcom/opensource/mm-drivers/hw_fence/Module.symvers                                                                         /home/dpi/qb5_8814/workspace/P4_1716/android/out/vendor/qcom/opensource/mm-drivers/sync_fence/Module.symvers                                                                         /home/dpi/qb5_8814/workspace/P4_1716/android/out/vendor/qcom/opensource/mm-drivers/msm_ext_display/Module.symvers                                                                         /home/dpi/qb5_8814/workspace/P4_1716/android/out/vendor/qcom/opensource/securemsm-kernel/Module.symvers                                                                         "
                        # for Audio(techpack) driver build
                        export MODNAME=audio_dlkm

                        export KBUILD_EXT_MODULES="../vendor/qcom/opensource/mm-drivers/msm_ext_display                           ../vendor/qcom/opensource/mm-drivers/sync_fence                           ../vendor/qcom/opensource/mm-drivers/hw_fence                           ../vendor/qcom/opensource/mmrm-driver                           ../vendor/qcom/opensource/securemsm-kernel                           ../vendor/qcom/opensource/display-drivers/msm                           ../vendor/qcom/opensource/audio-kernel                           ../vendor/qcom/opensource/camera-kernel                           "

        - Start to trigger build
                3. build kernel
                        RECOMPILE_KERNEL=1 ./kernel_platform/build/android/prepare_vendor.sh sec ${TARGET_PRODUCT}


2. Output files
        - Kernel : arch/${__arch_name}/boot/Image
        - module : drivers/*/*.ko

3. How to Clean
        Change to OUTPUT_DIR folder
        EX) /home/dpi/qb5_8814/workspace/P4_1716/android/out/target/product/dm3q/out
        $ make clean
################################################################################
