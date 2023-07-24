# Python-Based-Network-Ping-Sweeper

The primary purpose of the code is to perform a ping sweep, which literally means all it does is send a single ping packet (ping -c 1) to each host within the specified IP range to check if the hosts are reachable. For this example we used the ol' reliable IP Adresses ranges of 192.168.1.1 through 192.168.1.254 which are commonly used for local networks.

Here is a breakdown I created with the help of ChatGPT 3.5 of what each line of this code means.

```python
import subprocess
```
This line imports the `subprocess` module, which allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes. In our case, we will use it to execute the ping command.

```python
def ping_host(ip):
```
This line defines a function called `ping_host` that takes an IP address as an argument. Functions are blocks of reusable code that perform a specific task. Here, `ping_host` will be responsible for executing the ping command for a given IP address.

```python
    result = subprocess.call(['ping', '-c', '1', ip], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
```
This line uses the `subprocess.call()` function to execute the ping command. The `subprocess.call()` function takes a list of arguments, where each element represents a part of the command to be executed. In this case, we are calling the ping command with the following arguments:
- `'ping'`: The command to execute.
- `'-c'`: An option for specifying the number of packets to send.
- `'1'`: The value of the `-c` option, which specifies that we want to send only one ping packet.
- `ip`: The IP address of the host we want to ping.

We also use `stdout=subprocess.DEVNULL` and `stderr=subprocess.DEVNULL` to suppress the output of the ping command. We only need the return code to determine if the ping was successful or not.

The `result` variable will store the return code of the ping command. A return code of `0` indicates that the ping was successful, while a non-zero return code indicates that the ping failed.

```python
    if result == 0:
        return True
    else:
        return False
```
This code block checks the value of `result` and returns `True` if the ping was successful (i.e., `result` is `0`), and `False` if the ping failed (i.e., `result` is non-zero).

```python
def main():
```
This line defines another function called `main`. The `main` function is the entry point of our script. It will be called when we run the script.

```python
    start_ip = "192.168.1.1"
    end_ip = "192.168.1.254"
```
These lines define two variables `start_ip` and `end_ip`, which represent the beginning and end of the IP range we want to scan. Modify these IP addresses to fit the range you want to scan.

```python
    print(f"Scanning IP range from {start_ip} to {end_ip}")
```
This line prints a message to the console, displaying the IP range that will be scanned.

```python
    for i in range(int(start_ip.split('.')[-1]), int(end_ip.split('.')[-1])+1):
```
This line starts a `for` loop that will iterate through a range of numbers. The `range()` function generates a sequence of numbers from `start` to `stop-1`. Here, we are using `start_ip` and `end_ip` to define the range.

`int(start_ip.split('.')[-1])` extracts the last part of the IP address (the last octet) and converts it to an integer. Similarly, `int(end_ip.split('.')[-1])+1` extracts the last octet of the end IP address and adds 1 to it. This is done to include the end IP in the range, as the `range()` function stops at `stop-1`.

```python
        ip = '.'.join(start_ip.split('.')[:-1] + [str(i)])
```
This line constructs the full IP address to be pinged by combining the first three octets (obtained from `start_ip.split('.')[:-1]`) with the current value of `i` (the last octet) converted to a string.

```python
        if ping_host(ip):
```
This line calls the `ping_host()` function with the constructed IP address (`ip`) as an argument to check if the host is reachable.

```python
            print(f"Host {ip} is reachable.")
```
If the `ping_host()` function returns `True`, it means the host is reachable, and this line will print a message indicating that the host is reachable.

```python
        else:
```
If the `ping_host()` function returns `False`, it means the host is not reachable, and this line will be executed.

```python
            print(f"Host {ip} is not reachable.")
```
This line will print a message indicating that the host is not reachable.

```python
if __name__ == "__main__":
    main()
```
This block of code checks whether the script is being run directly (as opposed to being imported as a module). If it is the main script being run, it calls the `main()` function to start the ping sweep.

That's it folks I'd like to think you got it by now, and even more, that it's an employer looking at this and saying sheesh let's hire this dude lol.
#Done.
