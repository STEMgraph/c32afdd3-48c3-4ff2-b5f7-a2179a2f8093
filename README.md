<!---
{
  "id": "c32afdd3-48c3-4ff2-b5f7-a2179a2f8093",
  "depends_on": ["df08f299-5635-4e4d-8af1-632e-426614174000"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-07-03",
  "keywords": ["C", "pointers", "int", "char", "float", "pointer arithmetic", "address-of", "dereference"]
}
--->

# Pointers to `int`, `char`, and `float` in C

> In this exercise you will learn how to declare and initialize pointers to `int`, `char`, and `float`, use the address-of (`&`) and dereference (`*`) operators, and perform pointer arithmetic with scalar variables.

## Introduction

A **pointer** in C is a variable that holds the memory address of another variable. Pointers enable low-level memory access, dynamic data structures, and efficient parameter passing. Because each pointer has a specific type, pointer arithmetic automatically scales by the size of the pointed-to type.

To declare and initialize a pointer:

```c
int    i   = 42;
char   c   = 'A';
float  f   = 3.14f;

int   *iptr = &i;
char  *cptr = &c;
float *fptr = &f;
```

Dereferencing a pointer (`*p`) accesses the object at that address:

```c
printf("i = %d, at %p\n", *iptr, (void*)iptr);
*cptr = 'Z';
*fptr = 2.71f;
```

Pointer arithmetic expressions like `iptr + n`, `cptr + n`, or `fptr + n` compute addresses offset by `n * sizeof(*p)` bytes:

```
(p + n) == (char*)p + n * sizeof(*p)
```

This behavior ensures `iptr + 1` moves by `sizeof(int)` bytes, while `cptr + 1` moves by 1 byte.

### Further Readings and Other Sources

1. Kernighan & Ritchie, *The C Programming Language*, section 5.7.
2. ISO/IEC 9899:2011 Standard, sections on Pointers and Expressions.
3. cppreference.com, "Pointer arithmetic": [https://en.cppreference.com/w/c/language/operator\_arithmetic](https://en.cppreference.com/w/c/language/operator_arithmetic)
4. YouTube, "C Pointers Tutorial": [https://www.youtube.com/watch?v=KJgsSFOSQv0](https://www.youtube.com/watch?v=KJgsSFOSQv0)

## Tasks

### Task 1: Declaring and Using Pointers

**Problem:** Write a program that declares one `int`, one `char`, and one `float` variable along with corresponding pointers. Initialize the pointers and print each pointer’s address and the value obtained by dereferencing it.

**Solution Steps:**

1. Create `pointer_demo.c`.
2. Add:

   ```c
   #include <stdio.h>

   int main(void) {
       int    i   = 42;
       char   c   = 'A';
       float  f   = 3.14f;

       int   *iptr = &i;
       char  *cptr = &c;
       float *fptr = &f;

       printf("Address of i: %p, value: %d\n", (void*)iptr, *iptr);
       printf("Address of c: %p, value: %c\n", (void*)cptr, *cptr);
       printf("Address of f: %p, value: %.2f\n", (void*)fptr, *fptr);
       return 0;
   }
   ```
3. Compile and run:

   ```bash
   gcc pointer_demo.c -o pointer_demo
   ./pointer_demo
   ```

---

### Task 2: Pointer Arithmetic with Integers

**Problem:** Given an `int` variable `i = 100` and pointer `ip = &i`, assume `ip` holds the address `0x1000` and `sizeof(int) = 4`. Compute the addresses of `ip + 1` and `ip + 2`.

**Solution Steps:**

1. `ip + 1` advances by 4 bytes: `0x1000 + 4 = 0x1004`.
2. `ip + 2` advances by 8 bytes: `0x1000 + 8 = 0x1008`.
3. Verify in code using `printf("%p\n", (void*)(ip + n));`.

---

### Task 3: Comparing Pointer Arithmetic for `char`, `int`, and `float`

**Problem:** For `char c; char *cp = &c;`, `int i; int *ip = &i;`, and `float f; float *fp = &f;`, assume their base addresses are `0x2000`, `0x3000`, and `0x4000` respectively, with `sizeof(int) = sizeof(float) = 4`, `sizeof(char) = 1`. Compute the address of each pointer plus `n = 3`.

**Solution Steps:**

1. `cp + 3`: `0x2000 + 3 × 1 = 0x2003`.
2. `ip + 3`: `0x3000 + 3 × 4 = 0x300C`.
3. `fp + 3`: `0x4000 + 3 × 4 = 0x400C`.

## Questions

1. Explain why `ip + 1` and `cp + 1` yield different byte offsets.
2. How would you cast a `void*` (e.g., from `malloc`) to an `int*` and then dereference it?
3. What are the dangers of dereferencing an uninitialized pointer?
4. Given `float *fp`, derive a general formula for the byte offset of `fp + n` relative to `fp`.
5. Why must you cast pointers to `void*` when printing with `%p`?

## Advice

Mastering pointers is essential for C programming, as they provide direct memory access and enable efficient data structures. Always initialize your pointers before use to avoid undefined behavior, and use `size_t` for pointer arithmetic indices. When printing pointers, cast to `void*` and use `%p` for portability. Practice by experimenting with different types and pointer operations to deepen your understanding of how C handles memory addresses.
