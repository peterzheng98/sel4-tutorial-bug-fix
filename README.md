# sel4-tutorial-bug-fix
We all like seL4.

## Tutorial: crossvm

### generate and build
``````
./init --tut camkes-vm-crossvm
ninja
``````

If the following error occurred, make some little modification on `CMakeLists.txt`.
``````
CMake Error at CMakeLists.txt:20 (message):
  This application is only supported on x86_64
Call Stack (most recent call first):
  /******/sel4-cross-vms/projects/sel4-tutorials/Findsel4-tutorials.cmake:23 (include)
  CMakeLists.txt:3 (sel4_tutorials_regenerate_tutorial)
``````

Modification on CMakeLists.txt(`/path/to/repo/root/camkes-vm-crossvm/CMakeLists.txt`)
``````
-if(NOT "${KernelX86Sel4Arch}" STREQUAL "x86_64")
+if(NOT "${KernelSel4Arch}" STREQUAL "x86_64")
``````
Then execute `cmake -G Ninja -DTUT_ARCH=x86_64 -DFORCE_IOMMU=ON -DTUTORIAL_DIR=camkes-vm-crossvm -C ../projects/sel4-tutorials/settings.cmake /path/to/repo/root/camkes-vm-crossvm` in `/path/to/repo/root/camkes-vm-crossvm_build`
