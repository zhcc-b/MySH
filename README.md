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
import time
from huskylib import HuskyLensLibrary
from pubnub.pubnub import PubNub
from pubnub.pnconfiguration import PNConfiguration

# ID → Name mapping
id_name_map = {
    1: "Alice",
    2: "Bob",
    3: "Charlie"
}

# Initialize Huskylens (I2C)
hl = HuskyLensLibrary("I2C", "", address=0x32)

# Setup PubNub configuration
pnconfig = PNConfiguration()
pnconfig.subscribe_key = "sub-c-600de055-e08b-4dfd-8f69-231ee45b2313"
pnconfig.publish_key = "pub-c-cc09a5e0-ae7e-4f0b-91ba-3c06deac8056"
pnconfig.uuid = "z728"

pubnub = PubNub(pnconfig)
channel = "zhaox207"

def publish_result(name):
    message = {"recognized_name": name}
    pubnub.publish().channel(channel).message(message).sync()
    print(f"Published to PubNub: {message}")

def main():
    print("Starting Huskylens → PubNub recognition loop. Press Ctrl+C to stop.")
    while True:
        try:
            hl.request()
            if hl.available():
                blocks = hl.learned_blocks()
                for block in blocks:
                    name = id_name_map.get(block.ID, f"Unknown ID: {block.ID}")
                    print(f"Detected: {name}")
                    publish_result(name)
            else:
                print("No object detected.")
            time.sleep(1)
        except KeyboardInterrupt:
            print("Program stopped by user.")
            break
        except Exception as e:
            print(f"Error: {e}")

if __name__ == "__main__":
    main()

```

### Technologies & System Calls Used  
- **C Programming**  
- **System Calls**: `fork()`, `execvp()`, `waitpid()`, `pipe()`, `dup2()`, `kill()`, `sigaction()`  
- **Networking**: `socket()`, `bind()`, `listen()`, `accept()`, `connect()`  
- **Process Management**: Background processes, job control (`ps`, `kill`)  
- **File I/O & Redirection**: `open()`, `close()`, `read()`, `write()`  
