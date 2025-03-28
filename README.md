## MySH: A Custom Unix Shell in C  

### Introduction  
**MySH** is a lightweight Unix shell implemented in C, featuring built-in commands, process control, command chaining, and network-based client-server communication. This project demonstrates low-level system programming, process management, and inter-process communication (IPC) techniques.  

### Features  
✅ **Built-in Commands**: Supports essential shell commands including `echo`, `cat`, `wc`, `ls`, `cd`, `ps`, and `kill`.  
✅ **Process Management**: Handles background processes, signal handling, and job control.  
✅ **Command Pipelining**: Implements IPC with `dup2` and pipes for executing chained commands.  
✅ **Networking Support**: Includes a TCP-based client-server model for remote command execution.  
✅ **Variable Management**: Supports shell variables for command customization.  

### Project Structure  
- **`mysh.c`** - Entry point for the shell, handles user input and execution flow.  
- **`builtins.c/h`** - Implements built-in shell commands.  
- **`commands.c/h`** - Manages command parsing and execution, including background processes.  
- **`io_helpers.c/h`** - Provides input/output utilities and error handling.  
- **`variables.c/h`** - Implements shell variable storage and retrieval.  
- **`Makefile`** - Automates compilation and builds the project.  

### Installation & Usage  
#### Build the Project  
```sh
git clone https://github.com/yourusername/MySH.git
cd MySH
make
```
#### Run the Shell  
```sh
./mysh
```
#### Example Commands  
```sh
mysh$ echo "Hello, World!"
Hello, World!

mysh$ ls | wc -l
```
#### Start a TCP Server  
```sh
mysh$ start-server 8080
```
#### Connect a Client  
```sh
mysh$ start-client 8080 127.0.0.1
```

```sh
def printObjectNicely(obj):
    count = 1
    if isinstance(obj, list):
        for i in obj:
            name = id_name_map.get(i.ID, f"Unknown ID: {i.ID}")
            print(f"\tBLOCK_{count} : Name = {name}")
            print(f"\tPosition: x={i.x}, y={i.y}, width={i.width}, height={i.height}\n")
            count += 1
    else:
        name = id_name_map.get(obj.ID, f"Unknown ID: {obj.ID}")
        print(f"\tBLOCK_{count} : Name = {name}")
        print(f"\tPosition: x={obj.x}, y={obj.y}, width={obj.width}, height={obj.height}\n")
```

### Technologies & System Calls Used  
- **C Programming**  
- **System Calls**: `fork()`, `execvp()`, `waitpid()`, `pipe()`, `dup2()`, `kill()`, `sigaction()`  
- **Networking**: `socket()`, `bind()`, `listen()`, `accept()`, `connect()`  
- **Process Management**: Background processes, job control (`ps`, `kill`)  
- **File I/O & Redirection**: `open()`, `close()`, `read()`, `write()`  
