# 📚 libft

> A custom C standard library implementation compiling essential data structures, memory manipulation primitives, dynamic string utilities, and linked list APIs into a reusable static library.

## 📖 Overview

`libft` is the foundational project of the 42 software engineering curriculum. It serves as a custom implementation of standard C library (`libc`) functions along with additional dynamic memory, string manipulation, and abstract data structure (linked list) utilities. Compiled into a static archive (`libft.a`), this library acts as the baseline core dependency for all subsequent low-level C projects.

## ⚙️ Technical Standards & Constraints

- **Language:** C (compiled with `gcc -Wall -Wextra -Werror`).
- **Output Artifact:** Compiled into a static library archive (`libft.a`) using `ar rcs`.
- **Allowed Functions:** Primitive POSIX system calls (`write`), heap management (`malloc`, `free`).
- **Memory Safety:** 100% leak-free execution across dynamic string manipulations, array splits, and linked list destruction routines (audited via Valgrind).
- **Standards:** 100% compliant with 42's **Norminette** coding standard.

---

## 🗺️ Function Modules & Categorization

| Module | Core Functions | Technical Focus |
| :--- | :--- | :--- |
| **Character Checks & Conversions** | `ft_isalpha`, `ft_isdigit`, `ft_isalnum`, `ft_isascii`, `ft_isprint`, `ft_toupper`, `ft_tolower` | ASCII table boundary validation and case transformations. |
| **Memory Manipulation** | `ft_memset`, `ft_bzero`, `ft_memcpy`, `ft_memmove`, `ft_memchr`, `ft_memcmp`, `ft_calloc` | Raw byte pointer manipulation, buffer initializations, overlapping memory safety (`memmove`), and safe zeroed heap allocations (`calloc`). |
| **String Operations** | `ft_strlen`, `ft_strlcpy`, `ft_strlcat`, `ft_strchr`, `ft_strrchr`, `ft_strncmp`, `ft_strnstr`, `ft_strdup`, `ft_atoi` | Null-terminated buffer traversal, bounded copy/concatenation, substring searches, dynamic string duplicates, and ASCII-to-integer parsing. |
| **Non-Standard Utilities** | `ft_substr`, `ft_strjoin`, `ft_strtrim`, `ft_split`, `ft_itoa`, `ft_strmapi`, `ft_striteri` | Dynamic string allocations, string trimming, delimiter-based multi-string splitting (`ft_split`), integer-to-string formatting, and functional string mappings. |
| **File Descriptor I/O** | `ft_putchar_fd`, `ft_putstr_fd`, `ft_putendl_fd`, `ft_putnbr_fd` | Unbuffered character, string, and integer output written directly to target file descriptors (`stdin`, `stdout`, `stderr`, or file streams). |
| **Linked List API (Bonus)** | `ft_lstnew`, `ft_lstadd_front`, `ft_lstsize`, `ft_lstlast`, `ft_lstadd_back`, `ft_lstdelone`, `ft_lstclear`, `ft_lstiter`, `ft_lstmap` | Abstract singly linked list implementation handling dynamic node creation, insertion, traversal, element mapping, and complete memory teardowns. |

---

## 🛠️ Quickstart & Integration Example

### Testing Library Functions (`main.c`)

You can test `libft` by creating a test runner main file:

```c
#include <stdio.h>
#include <stdlib.h>
#include "libft.h"

int main(void)
{
    // String join and split test
    char  *str = "C,System,Programming,42";
    char  **split_array;
    int   i;

    printf("--- libft Split Test ---\n");
    split_array = ft_split(str, ',');
    if (!split_array)
        return (1);

    i = 0;
    while (split_array[i])
    {
        printf("[%d]: %s\n", i, split_array[i]);
        free(split_array[i]);
        i++;
    }
    free(split_array);

    // Dynamic int to ASCII test
    char *num_str = ft_itoa(-4242);
    printf("\n--- libft itoa Test ---\nConverted: %s\n", num_str);
    free(num_str);

    return (0);
}

# Clone the repository
git clone [https://github.com/your-username/libft.git](https://github.com/your-username/libft.git)
cd libft

# Compile static library libft.a (includes mandatory parts)
make

# Compile static library including linked list bonus functions
make bonus

# Compile test runner against the static library
gcc -Wall -Wextra -Werror main.c libft.a -o libft_test

# Run test executable
./libft_test

# Clean object files
make clean

# Clean object files and static library archive
make fclean

# Recompile the library from scratch
make re
