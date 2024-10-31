# Fork Example in C

This code demonstrates the use of the `fork()` function in C, which allows for the creation of a new process (child process) from an existing process (parent process). This README provides a line-by-line explanation of the code.

## Code

```c
#include <unistd.h>
#include <sys/types.h>
#include <stdio.h>

int main() {
    pid_t q;
    printf("before fork\n");
    q = fork();

    if (q < 0) {
        // fork failed
        perror("Fork failed");
        return 1;
    } else if (q == 0) {
        // Child process
        printf("I am the child process with ID: %d\n", getpid());
        printf("My parent's ID is: %d\n", getppid());
    } else {
        // Parent process
        printf("I am the parent process with ID: %d\n", getpid());
        printf("My child's ID is: %d\n", q);
    }

    printf("Process complete\n");
    return 0;
}
```

## Explanation

### 1. Include Libraries
- **`#include <unistd.h>`**: Provides access to POSIX API, including `fork()`.
- **`#include <sys/types.h>`**: Defines data types like `pid_t` for storing process IDs.
- **`#include <stdio.h>`**: Standard I/O library for using `printf()`.

### 2. Main Function
- **`int main()`**: Entry point of the program.

### 3. Declare PID Variable
- **`pid_t q;`**: Declares `q` to store the process ID returned by `fork()`.

### 4. Print Before Fork
- **`printf("before fork\n");`**: Indicates the program’s start.

### 5. Create a New Process
- **`q = fork();`**: Creates a new process:
  - Returns `0` to the child process.
  - Returns the child’s PID to the parent process.
  - Returns `-1` if `fork()` fails.

### 6. Error Handling for Fork Failure
```c
if (q < 0) {
    perror("Fork failed");
    return 1;
}
```
- Checks if `fork()` failed (returns `-1`).
- **`perror("Fork failed");`**: Prints an error message if `fork()` failed.
- **`return 1;`**: Indicates unsuccessful execution.

### 7. Child Process Block
```c
else if (q == 0) {
    printf("I am the child process with ID: %d\n", getpid());
    printf("My parent's ID is: %d\n", getppid());
}
```
- Executes in the child process (when `q == 0`).
- Prints the child’s process ID (`getpid()`) and the parent’s process ID (`getppid()`).

### 8. Parent Process Block
```c
else {
    printf("I am the parent process with ID: %d\n", getpid());
    printf("My child's ID is: %d\n", q);
}
```
- Executes in the parent process (where `q` holds the child’s PID).
- Prints the parent’s process ID (`getpid()`) and the child’s process ID (`q`).

### 9. Process Completion
```c
printf("Process complete\n");
return 0;
```
- Printed by both the parent and child, marking each process’s end.
- **`return 0;`**: Indicates successful program completion.

---

## Output Example

When you run this code, you may see output similar to this:

```
before fork
I am the parent process with ID: 62678 
My child's ID is: 62679 
Process complete
I am the child process with ID: 62679
My parent's ID is: 1277 
Process complete
```

Each output sequence may vary based on process scheduling but will include messages from both the parent and child processes.
