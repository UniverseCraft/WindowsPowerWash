# PowerWash (PowerShell script)
Remove bloatware from Windows and optimize for low latency and high performance

## Setup
- Download `PowerWash.ps1`
- Make sure your [`ExecutionPolicy`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.3) allows scripts to run

## Usage
- Open a PowerShell prompt as an Administrator
- `cd` to the directory containing `PowerWash.ps1`
- Run `.\PowerWash.ps1 /?` to see usage information, or `.\PowerWash.ps1 /all /autorestart` to run the full PowerWash suite and restart when done.

## How It Works
The default Windows installation has to cater to a very wide variety of users, and generally makes tradeoffs that sacrifice some degree of performance and responsiveness in exchange for power management, data collection, etc.

PowerWash modifies various aspects of your Windows installation. Instead of compromising performance for power efficiency, it configures your system to compromise power efficiency for low latency and high performance. (Note: Many of the changes do not apply when on battery)

Current features include:
- Running Microsoft's built-in system file integrity checks to repair any corrupted system files
- Installing Group Policy editor, which presents a straightforward and well-documented interface to make system changes without manually editing the registry. Group Policy editor is a Microsoft product but does not come installed by default on Home editions of Windows.
- Disabling the high precision event timer (can improve DPC latency)
- Disabling network adapter packet coalescing (can improve DPC latency)
- Disabling automatic Windows updates (because nobody likes being interrupted)
- Disabling Windows telemetry (can waste resources)
- Applying more aggressive multimedia settings (can improve performance of pro audio tasks)
- Enabling Microsoft's "Ultimate" performance power plan along with additional highly aggressive performance settings
- Enabling message-signaled interrupts on all devices that support them (can improve ISR latency)
- Enabling interrupts from ACPI devices to be spread across all processors (can improve DPC latency from `acpi.sys`)
- Prioritizing interrupts from devices like GPU and PCIe controller (may improve DPC/ISR latency)
- Checking for IRQ conflicts (these cannot be resolved automatically, though)
- Checking if a third-party antivirus is installed (Windows Defender is faster and better - third party antivirus must be uninstalled manually, though)

## Suggestions and Tips
- I recommend you use programs like [LatencyMon](https://www.resplendence.com/latencymon) and [WhySoSlow](https://www.resplendence.com/whysoslow) to benchmark your system before and after running PowerWash.
- This script should be accompanied by a manual review of preinstalled programs, devices, services, etc.
- Adequate thermal management is imperative to stable device functioning. Make sure your device is being cooled adequately.
- You can also overclock CPU/GPU/RAM if needed, but this is a "brute force" approach and you should try to get performance as high as possible before resorting to this
- Always back up your system before running PowerWash or making any other system configuration changes.
- Obviously, all of this is "use at your own risk"

