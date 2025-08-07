# wuauserv-services ⚙️

This repository provides quick fixes and restore `.reg` files to solve common Windows Update service (`wuauserv`) errors, especially the **System Error 126 (ERROR_MOD_NOT_FOUND)**.

---

## About this project

Windows Update is an essential service for keeping your system secure and up to date.  
However, sometimes the service fails to start due to registry misconfigurations or missing files, causing errors like:

- **System Error 126: The specified module could not be found**  
- **System Error 2: The system cannot find the file specified**

These issues often relate to the wrong DLL file set in the registry or corrupted service parameters.

---

## What is inside?

- [`fix-ERROR_MOD_NOT_FOUND.reg`](System%20Error%20126/fix-ERROR_MOD_NOT_FOUND.reg)  
  Corrects the registry entry for `ServiceDll` to `%SystemRoot%\System32\wuaueng.dll`, fixing Error 126.

- [`restore-wuauserv.reg`](System%20Error%202/restore-wuauserv.reg)  
  Restores default registry parameters of the Windows Update service in case of more severe issues.

---

## How to use

1. **Backup your registry (recommended):**  
   Before applying any fixes, export the key for safety:  
   ```reg export HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\wuauserv wuauserv-backup.reg```

2. **Run the appropriate `.reg` file as Administrator:**  
- Right-click the `.reg` file → *Run as Administrator*  
- Confirm the prompts to merge the file into your registry.

3. **Restart your computer** for changes to take effect.

4. **Try starting the service:**  
Open a Command Prompt as Administrator and run:  
```net start wuauserv```

---

## Additional recommendations

If issues persist, try running these system tools to repair corrupted system files:

```powershell
sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
```

Run them in an elevated command prompt and restart your machine after completion.

---

## License
This project is provided as-is without any warranty. Use at your own risk.
