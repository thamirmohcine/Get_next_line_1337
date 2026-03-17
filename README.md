# Get_next_line_1337

`get_next_line` is a C function that reads and returns one line at a time from a file descriptor, including the trailing newline when present. This repository contains both the mandatory implementation and the bonus version that supports multiple file descriptors simultaneously.

---

## 📌 Project Overview

This project implements:

- A robust line-by-line reader for low-level file descriptors
- Internal static buffering between calls
- Safe memory handling for dynamic string assembly
- Bonus support for parallel reads across multiple FDs

Function prototype:

```c
char *get_next_line(int fd);
```

Behavior summary:

- Returns the next line from `fd` on each call
- Includes `\n` if it exists before end-of-file
- Returns `NULL` on EOF or error

---

## 📂 Repository Structure

```text
.
├── get_next_line.c
├── get_next_line.h
├── get_next_line_utils.c
├── get_next_line_bonus.c
├── get_next_line_bonus.h
├── get_next_line_utils_bonus.c
└── README.md
```

---

## 📦 Installation

No `package.json` or `requirements.txt` is needed for this project.
This is a pure C project and can be built with `cc`.

### 1) Clone

```bash
git clone https://github.com/thamirmohcine/Get_next_line_1337.git
cd Get_next_line_1337
```

### 2) Compile (Mandatory)

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
	get_next_line.c get_next_line_utils.c main.c -o gnl
```

### 3) Compile (Bonus)

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
	get_next_line_bonus.c get_next_line_utils_bonus.c main_bonus.c -o gnl_bonus
```

> `main.c` / `main_bonus.c` are test drivers you provide locally.

---

## 🚀 Usage

Below is a simple usage example around the project’s main API (`get_next_line`):

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include "get_next_line.h"

int main(void)
{
		int   fd;
		char  *line;

		fd = open("example.txt", O_RDONLY);
		if (fd < 0)
				return (1);

		line = get_next_line(fd);
		while (line)
		{
				printf("%s", line);
				free(line);
				line = get_next_line(fd);
		}

		close(fd);
		return (0);
}
```

Run:

```bash
./gnl
```

---

## ⚙️ Notes

- You can tune memory/read behavior with `BUFFER_SIZE` at compile time.
- Mandatory version uses one static buffer.
- Bonus version uses one static buffer per file descriptor (`OPEN_MAX`).
- Always `free()` each returned line to avoid leaks.

---

## ✅ 42 Project Context

This repository follows the 42 school `get_next_line` project constraints and coding style, focusing on:

- File descriptor handling
- Static state management
- Dynamic memory safety
- Utility reimplementation (`ft_strlen`, `ft_strdup`, `ft_strjoin`, ...)

---

## 👤 Author

**mthamir**  
1337 (42 Network) Student
