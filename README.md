# Virtual Memory Simulator 
This repository contains a Python simulation of virtual memory management using two page replacement algorithms: FIFO (First-In-First-Out) and LRU (Least Recently Used). The simulator also includes a basic implementation of demand paging and copy-on-write mechanisms.
## Overview

Virtual memory allows a computer to compensate for shortages of physical memory by temporarily transferring data from random access memory (RAM) to disk storage. The concept of Copy-on-Write (COW) optimizes memory usage by allowing multiple processes to share the same pages in memory until a write operation occurs.

This simulator demonstrates how virtual memory operates with:
- **Demand Paging**: Loading pages into memory only when they are needed, which can cause page faults.
- **Copy-on-Write**: Handling write operations by creating a copy of the page when a write occurs.
- **FIFO Page Replacement**: Replaces the oldest page in memory when a new page needs to be loaded.
- **LRU Page Replacement**: Replaces the least recently used page in memory when a new page needs to be loaded.
## Classes and Methods

### `Page`

Represents a page in memory.
- `number`: The page number.
- `is_cow`: Boolean flag indicating if the page is marked as copy-on-write.

### `VirtualMemorySimulator`

Base class for the virtual memory simulator.
- `capacity`: The maximum number of pages that can be held in memory.
- `memory`: List of pages currently in memory.
- `page_faults`: Counter for the number of page faults.
- `page_map`: Dictionary mapping page numbers to `Page` objects.

#### Methods:
- `access_page(page_number, write=False)`: Access a page in memory, loading it if not present, and handling copy-on-write if necessary.
- `replace_page()`: Abstract method to be implemented by subclasses for page replacement.
- `display_state()`: Displays the current state of the memory.

### `FIFO_VirtualMemorySimulator`

Subclass of `VirtualMemorySimulator` that uses the FIFO page replacement algorithm.
- `replace_page()`: Replaces the oldest page in memory.

### `LRU_VirtualMemorySimulator`

Subclass of `VirtualMemorySimulator` that uses the LRU page replacement algorithm.
- `recent_usage`: List tracking the order of page usage.
- `access_page(page_number, write=False)`: Overrides the base method to update the recent usage list.
- `replace_page()`: Replaces the least recently used page in memory.
## Usage

### Sample Page Access Sequence

The following sample sequence demonstrates the page access pattern:
```python
page_sequence = [(7, False), (0, False), (1, False), (2, False), (0, True), 
                 (3, False), (0, True), (4, False), (2, False), (3, True), 
                 (0, True), (3, True), (2, False)]
capacity = 4
print("FIFO Page Replacement with Demand Paging and Copy-on-Write:")
fifo_simulator = FIFO_VirtualMemorySimulator(capacity)
for page_number, write in page_sequence:
    fifo_simulator.access_page(page_number, write)
fifo_simulator.display_state()
print("LRU Page Replacement with Demand Paging and Copy-on-Write:")
lru_simulator = LRU_VirtualMemorySimulator(capacity)
for page_number, write in page_sequence:
    lru_simulator.access_page(page_number, write)
lru_simulator.display_state()
#Outputs
![output](https://github.com/user-attachments/assets/21d177c3-863d-449e-a9dc-8894d7b719ca)
![output2](https://github.com/user-attachments/assets/822785fc-bfc2-4be1-9371-eb7deee80e97)
![output3](https://github.com/user-attachments/assets/8659d964-3e5f-40de-b7ae-f107ae99dee8)


![output](https://github.com/user-attachments/assets/24848316-4c83-4fb6-9a28-58ec15d6e058)
![output2](https://github.com/user-attachments/assets/687bf317-fb81-4583-bfe3-39f266245911)
![output3](https://github.com/user-attachments/assets/5667c0a7-2a3c-4a0d-b1b5-3732e99c35da)


