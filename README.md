# 📚 libft

> A custom C standard library implementation compiling essential data structures, memory manipulation primitives, dynamic string utilities, and linked list APIs into a reusable static library.

## 📖 Overview

`libft` is the foundational project of the 42 software engineering curriculum. The project focuses on recreating core functions of the C standard library (`libc`), along with additional dynamic memory, string parsing, and abstract data structure (linked list) utilities. Compiled into a static archive (`libft.a`), this library serves as a primary dependency across all subsequent low-level C system projects.

## ⚙️ Technical Standards & Constraints

- **Language:** C (compiled with `gcc -Wall -Wextra -Werror`).
- **Output Artifact:** Compiled into a static library archive (`libft.a`) using `ar rcs`.
- **Allowed System Calls:** Primitive POSIX system calls (`write`), heap memory allocation (`malloc`, `free`).
- **Memory Safety:** 100% leak-free execution across dynamic string allocations, array splits, and linked list destruction routines (audited via Valgrind).
- **Standards:** 100% compliant with 42's **Norminette** coding standard.

---

## 🗺️ Function Index & Implementation Details

### 1. Character Checks & Case Conversions

| Function | Description |
| :--- | :--- |
| `ft_isalpha` | Checks if the passed character is an alphabetic letter (`A-Z` or `a-z`). |
| `ft_isdigit` | Checks if the passed character is a decimal digit (`0-9`). |
| `ft_isalnum` | Checks if the passed character is alphanumeric (`A-Z`, `a-z`, or `0-9`). |
| `ft_isascii` | Checks if the passed character fits into the standard 7-bit ASCII table (`0-127`). |
| `ft_isprint` | Checks if the character is printable (including spaces). |
| `ft_toupper` | Converts a lowercase character to its corresponding uppercase letter. |
| `ft_tolower` | Converts an uppercase character to its corresponding lowercase letter. |

### 2. Memory Manipulation

| Function | Description |
| :--- | :--- |
| `ft_memset` | Fills the first $n$ bytes of a memory buffer with a constant byte value. |
| `ft_bzero` | Erases data in the first $n$ bytes of a memory block by setting them to zero (`\0`). |
| `ft_memcpy` | Copies $n$ bytes from source memory area to destination area (non-overlapping). |
| `ft_memmove` | Safely copies $n$ bytes between memory areas, handling overlapping memory buffers correctly. |
| `ft_memchr` | Scans a memory block for the first occurrence of a target byte value. |
| `ft_memcmp` | Compares two memory blocks byte by byte for a specified length. |
| `ft_calloc` | Allocates heap memory for an array of elements and initializes all bytes to zero. |

### 3. String Operations & Parsing

| Function | Description |
| :--- | :--- |
| `ft_strlen` | Calculates the total length of a null-terminated string. |
| `ft_strlcpy` | Copies up to `size - 1` characters from a string to a destination buffer, guaranteed null-terminated. |
| `ft_strlcat` | Appends a string to another with explicit buffer size safety, guaranteed null-terminated. |
| `ft_strchr` | Searches for the first occurrence of a character in a string. |
| `ft_strrchr` | Searches for the last occurrence of a character in a string. |
| `ft_strncmp` | Compares up to $n$ characters of two strings lexicographically. |
| `ft_strnstr` | Locates a needle substring within a haystack string, searching up to $n$ characters. |
| `ft_strdup` | Allocates dynamic heap memory and duplicates a null-terminated string. |
| `ft_atoi` | Parses an ASCII string representation into its corresponding signed integer value. |

### 4. Non-Standard Utilities & String Formatting

| Function | Description |
| :--- | :--- |
| `ft_substr` | Extracts a newly allocated substring from a string given a start index and maximum length. |
| `ft_strjoin` | Concatenates two strings into a newly allocated, null-terminated string. |
| `ft_strtrim` | Trims leading and trailing characters matching a target set from a string. |
| `ft_split` | Splits a string into an array of strings using a specified character delimiter. |
| `ft_itoa` | Converts a signed integer into a dynamically allocated ASCII string representation. |
| `ft_strmapi` | Applies a mapping function to each character of a string to construct a new allocated string. |
| `ft_striteri` | Applies an in-place modification function to each character of a string by passing its index and pointer. |

### 5. File Descriptor I/O

| Function | Description |
| :--- | :--- |
| `ft_putchar_fd` | Outputs a single character to a specified file descriptor (`fd`). |
| `ft_putstr_fd` | Outputs a string to a specified file descriptor (`fd`). |
| `ft_putendl_fd` | Outputs a string followed by a newline (`\n`) to a specified file descriptor (`fd`). |
| `ft_putnbr_fd` | Outputs a signed integer as text to a specified file descriptor (`fd`). |

### 6. Linked List API (Bonus)

| Function | Description |
| :--- | :--- |
| `ft_lstnew` | Allocates and initializes a new node element containing user data (`content`). |
| `ft_lstadd_front` | Inserts a new node at the beginning of a singly linked list. |
| `ft_lstsize` | Counts and returns the total number of elements in a linked list. |
| `ft_lstlast` | Returns a pointer to the last node of a linked list. |
| `ft_lstadd_back` | Appends a new node to the end of a linked list. |
| `ft_lstdelone` | Deallocates a single node's content using a custom free function and frees the node itself. |
| `ft_lstclear` | Deallocates and frees an entire linked list sequence and all its node contents. |
| `ft_lstiter` | Iterates through a linked list, applying a function to each node's content. |
| `ft_lstmap` | Iterates through a list, applies a function to each element, and creates a new transformed linked list. |

---

## 🛠️ Quickstart & Integration Example

### Testing Library Functions (`main.c`)

You can test `libft` utilities by linking them into a test runner:

```c
#include <stdio.h>
#include <stdlib.h>
#include "libft.h"

int main(void)
{
    // 1. Array splitting test
    char  *csv_input = "C,System,Programming,42";
    char  **tokens;
    int   i;

    printf("--- ft_split Demo ---\n");
    tokens = ft_split(csv_input, ',');
    if (tokens)
    {
        i = 0;
        while (tokens[i])
        {
            printf("Token [%d]: %s\n", i, tokens[i]);
            free(tokens[i]);
            i++;
        }
        free(tokens);
    }

    // 2. Integer formatting test
    char *num_str = ft_itoa(-4242);
    printf("\n--- ft_itoa Demo ---\nFormatted Integer: %s\n", num_str);
    free(num_str);

    return (0);
}

# Clone the repository
git clone [https://github.com/your-username/libft.git](https://github.com/your-username/libft.git)
cd libft

# Compile static library libft.a (mandatory routines)
make

# Compile static library including linked list bonus routines
make bonus

# Compile test application against the static library
gcc -Wall -Wextra -Werror main.c libft.a -o libft_test

# Execute test application
./libft_test

# Clean object files
make clean

# Clean object files and static library archive
make fclean

# Rebuild library from scratch
make re
