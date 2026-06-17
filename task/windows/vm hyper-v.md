### VM failed
```
[ 1 ] Import VM using old data VM
- Note path VM file resources 
- Delete VM in failover cluster manager and hyper-v manager
- Import VM from hyperv manager
  - Select the folder containing the VM
  - Select VM 
  - Choose import type: register the VM in-place (use the existing unique ID)
- Finish

[ 2 ] Create new VM using old data VM
- Note path VM file resources 
- Delete VM in failover cluster manager and hyper-v manager
- Create new VM from hyperv manager
  - Input VM name sama as folder VM resources name
  - Select volume folder that VM resources saved
  - Initiate spec VM
  - Select use an existing virtual hard disk, and select vhdx file in the VM resources folder
- Finish
```

### Case VM Failed
- <img width="838" height="221" alt="image" src="https://github.com/user-attachments/assets/302fa7b1-e10b-48bb-b45f-8b6824ee7a6d" /> <br>
  Jika terjadi vm Failed, contoh VM-HQ-GASQT-3 <br>
  <img width="919" height="260" alt="image" src="https://github.com/user-attachments/assets/fc24193e-9003-4f20-803c-c6aceb2d2780" />
  Cek di hyper-v apakah vm nya ada, jika tidak ada import vm atau create new vm (Create new vm jika file *.vmcx dan *.xml tidak ada di folder file vm di volume)
