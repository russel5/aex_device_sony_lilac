Device configuration for Sony Xperia XZ1 Compact (lilac)
========================================================

Description
-----------

This repository is for AEX 10.x on Sony Xperia XZ1 Compact (lilac).

How to build AEX
----------------------

* Make a workspace:

        mkdir -p ~/aex/repo
        cd ~/aex/repo

* Initialize the repo:

        repo init -u git://github.com/AospExtended/manifest.git -b 10.x

* Create a local manifest:

        vim .repo/local_manifests/roomservice.xml

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <!-- SONY -->
            <project name="russel5/aex_kernel_sony_msm8998" path="kernel/sony/msm8998" remote="github" revision="10.x" />
            <project name="russel5/aex_device_sony_common-treble" path="device/sony/common-treble" remote="github" revision="10.x" />
            <project name="russel5/aex_device_sony_yoshino" path="device/sony/yoshino" remote="github" revision="10.x" />
            <project name="russel5/aex_device_sony_lilac" path="device/sony/lilac" remote="github" revision="10.x" />

            <!-- Pinned blobs for lilac -->
            <project name="russel5/aex_vendor_sony_lilac" path="vendor/sony/lilac" remote="github" revision="10.x" />
        </manifest>

* Sync the repo:

        repo sync

* Extract vendor blobs (this step not needed if you are take a blobs from my repo)

        cd device/sony/lilac
        ./extract-files.sh

* Setup the environment

        source build/envsetup.sh
        lunch aosp_lilac-userdebug

* Apply a patch (make camera key working. patch will be update, now it works at 06.05.2020)

		cp camerakey.patch ../../../frameworks/base/services/core/java/com/android/server/policy	
		cd ../../../frameworks/base/services/core/java/com/android/server/policy
		patch -p1 < camerakey.patch

* Build AEX

        make -j4 aex
