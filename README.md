Patches that help me build GSI

Use instructions : <a href="https://github.com/phhusson/treble_experimentations/wiki/How-to-build-a-GSI%3F">How to build GSI?</a>

I build using the manual way (helps to understand what's what)
  
  1. Repo init the rom you want to build GSI for.
      
      ```bash
      
      mkdir ~/gsi_rom &&  cd ~/gsi_rom
      repo init -u https://github.com/Havoc-OS/android_manifest.git -b ten (example)
      ```
  
  2. Add phh repos to your local_manifest
  
     ```bash
     
     git clone https://github.com/phhusson/treble_manifest .repo/local_manifests  -b android-10.0
     ```
     
     After git clone you need to delete replace.xml (.repo/local_manifests/replace.xml) if you're building any rom except AOSP GSI.
     
  3. Sync the source
     
     ```bash
     
     repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
     ```
  4. Apply patches.
     
     ```bash
     
     git am < file.patch 
     or
     patch -p1 < file.patch
     ```
  Нou can read for example <a href="https://www.devroom.io/2009/10/26/how-to-create-and-apply-a-patch-with-git/">here</a> 
  
  5. Edit the .mk for your ROM in device/phh/treble
  
     Can be used as an example havoc.mk, linaege.mk
     Call it by any name, for example evox.mk 
     and do
     
     ```bash
     
     bash generate.sh evox 
     ```
  6. Lunch the build variant you want (ex. treble_arm64_bvN-userdebug) and start the build
     
     ```bash
     
     . build/envsetup.sh
     lunch treble_arm64_bvN-userdebug
     WITHOUT_CHECK_API=true 
     make -j systemimage 
     ```
       
# Credits:
* [phhusson](https://github.com/phhusson)
* [eremitein](https://github.com/eremitein/treble-patches)
* [AndyCGYan](https://github.com/AndyCGYan)

