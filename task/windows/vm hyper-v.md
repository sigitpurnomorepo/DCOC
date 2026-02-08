### VM failed
1. Import VM using old data VM
```
- Note path VM file resources 
- Delete VM in failover cluster manager and hyper-v manager
- Import VM from hyperv manager
  - Select the folder containing the VM
  - Select VM 
  - Choose import type: register the VM in-place (use the existing unique ID)
- Finish

2. Create new VM using old data VM

- Note path VM file resources 
- Delete VM in failover cluster manager and hyper-v manager
- Create new VM from hyperv manager
  - Input VM name sama as folder VM resources name
  - Select volume folder that VM resources saved
  - Initiate spec VM
  - Select use an existing virtual hard disk, and select vhdx file in the VM resources folder
- Finish
```
