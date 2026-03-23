# Memory Optimizer

This tool optimizes memory allocation for AMD Ryzen AI Max+ Pro 395 (or similar APUs) by configuring TTM page pool settings.

## Main Method: Bash Script (Recommended)

The bash script (`setup_vram_grub.sh`) is the primary and most straightforward method. It automates the entire configuration process with elevated privileges.

### Features
- Detects system RAM automatically from `/proc/meminfo`
- Calculates recommended VRAM ceiling (leaves 16GB for system/CPU)
- Warns if allocation exceeds 90% of total RAM
- Automatically updates GRUB configuration
- Supports multiple distributions (Debian, Ubuntu, Fedora, Arch, CachyOS, CentOS/RHEL)
- Uses 4KB page size for accurate calculations

### Usage

```bash
sudo ./setup_vram_grub.sh [target_ram_gb]
```

Optional argument: `target_ram_gb` - specify VRAM directly (e.g., `sudo ./setup_vram_grub.sh 16`)

Example output:
```
--- AMD Ryzen AI Max+ Pro 395 Optimizer ---
Detected System RAM: 32.00 GB
Recommended VRAM Ceiling: 16 GB (Leaving 16GB for OS)

Enter target VRAM in GB [Default 16]: 

======================================
  TARGET: 16 GB
  PAGES:  4194304
======================================

Adding to /etc/default/grub:
  ttm.pages_limit=4194304 ttm.page_pool_size=4194304

Apply these changes? (y/N): y
Updating GRUB for ubuntu...
VRAM configuration applied successfully!
```

### Prerequisites
- Linux operating system
- Root access (required for GRUB modification)
- AMD GPU driver with TTM support

### Important Notes
- Always backup your GRUB config before making changes: `sudo cp /etc/default/grub /etc/default/grub.backup`
- After modifying GRUB, the script automatically runs `update-grub` or `grub2-mkconfig` depending on your distribution
- Allocating >90% of RAM to GPU may cause system instability or OOM kills
- Page size is calculated using standard 4KB page size (page_pool_size is in pages, not bytes)

## Alternative Method: Python Script

For users uncomfortable executing bash scripts with elevated privileges, a Python script (`Memory_Optimizer.py`) is available. It calculates the necessary values but requires manual GRUB configuration.

### Usage

```bash
python3 Memory_Optimizer.py
```

### Differences from Bash Script
- Only displays calculated values and GRUB parameters
- Does not modify system configuration
- Does not require root access for calculations
- Manual GRUB editing required after running

## Supported Hardware
- AMD Ryzen AI Max+ Pro 395 (and other APUs with shared memory)
- Linux systems using the AMDGPU driver with TTM (Translation Table Maps)
