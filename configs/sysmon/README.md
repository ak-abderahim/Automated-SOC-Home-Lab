## 📂 Repository Structure

The project files are organized into distinct folders for scannability and ease of deployment:

* **📁 `config/`** 
  * `sysmon-modular-config.xml` — A highly optimized, medium-verbosity template by Olaf Hartong. It defines exactly what malicious behaviors to monitor (like UAC bypasses and defense evasion) and what safe apps to ignore.
* **📁 `drivers/`** (or `bin/`)
  * `sysmon.exe` / `sysmon.sys` — The raw binary engines that hook into the Windows kernel to collect real-time event logs.
* **📁 `documentation/`**
  * `sysinternals_license.txt` — The official software license terms and data collection notices for the Microsoft Sysinternals suite.
