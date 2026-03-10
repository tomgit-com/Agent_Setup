# Memory Optimizer

A Python script to optimize memory allocation for AMD Ryzen AI Max+ Pro 395 (or similar APUs) by calculating appropriate TTM page pool settings.

## Features

- Detects system RAM automatically from `/proc/meminfo`
- Calculates recommended VRAM ceiling (leaves 16GB for system/CPU)
- Warns if allocation exceeds 90% of total RAM
- Displays GRUB parameters to add manually
- Uses 4KB page size for accurate calculations

## Usage

```bash
python Memory_Optimizer.py
```

Example output:
```
--- AMD Ryzen AI Max+ Pro 395 Optimizer ---
Detected System RAM: 32.00 GB
Recommended VRAM Ceiling: 16 GB (Leaving 16GB for OS)

Enter target VRAM in GB [Default 16]: 

=============================================
  TARGET: 16 GB
  PAGES:  4194304
=============================================

Add this to your GRUB_CMDLINE_LINUX_DEFAULT:
ttm.pages_limit=4194304 ttm.page_pool_size=4194304
```

The script will:
1. Detect your system RAM
2. Recommend a VRAM ceiling (Total RAM - 16GB system reserve)
3. Prompt for a target VRAM value (or use the recommendation)
4. Display the calculated page count (using 4KB page size)
5. Output the GRUB parameters to add: `ttm.pages_limit=<pages> ttm.page_pool_size=<pages>`

## Prerequisites

- Linux operating system
- Root access (for viewing `/proc/meminfo` and modifying GRUB)
- AMD GPU driver with TTM support

## Important Notes

- **Root access required** to modify GRUB configuration
- Always backup your GRUB config before making changes: `sudo cp /etc/default/grub /etc/default/grub.backup`
- After modifying GRUB, run: `sudo update-grub` and reboot
- Allocating >90% of RAM to GPU may cause system instability or OOM kills
- Page size is calculated using standard 4KB page size (page_pool_size is in pages, not bytes)

## Supported Hardware

- AMD Ryzen AI Max+ Pro 395 (and other APUs with shared memory)
- Linux systems using the AMDGPU driver with TTM (Translation Table Maps)
