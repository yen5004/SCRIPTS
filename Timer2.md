Timers 2

### #For a simple timer that displays on screen:

A simple timer that displays time, including seconds and nanoseconds:

![image1][(https://github.com/yen5004/SCRIPTS/blob/main/Untitled.png)

```bash
while true; do printf '%s\r' "$(date +%H:%M:%S:%N)"; done
# Press ctrl+c to exit
```

A simple timer that displays time, including seconds:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/367ee8fa-5ed0-4c82-90f7-44c7638843ee/Untitled.png)

```bash
while true; do printf '%s\r' "$(date +%H:%M:%S)"; done
# Press ctrl+c to exit
```

Plain timer:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/8dfc5198-aaed-4666-bdbe-e5653db22021/Untitled.png)

```jsx
# Another timer shows seconds:
start=$(date +%s)
while true; do
time="$(($(date +%s) - $start))"
printf '%s\r' "$(date -u -d "@$time" +%H:%M:%S)"
done
```

```bash
# This one ctrl + c must be entered to stop and display the timer
#Start:
time cat
# To stop press ctrl+c

```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/ea39f506-ed7f-4796-8ded-64087b42633d/Untitled.png)

oooor

Doesn't work for Kali: must ctrl + c  to stop and display time

```bash
time read
```

Like above, but works for Kali: must ctrl + c  to stop and display time

```bash
time (read)
```

Here's one using cursor movements that will rewrite the line to show a countdown:

works well, prints out “starting.. counts down, and then says done

```bash
c=5 # seconds to wait
REWRITE="\e[25D\e[1A\e[K"
echo "Starting..."
while [ $c -gt 0 ]; do
c=$((c-1))
sleep 1
echo -e "${REWRITE}$c"
done
echo -e "${REWRITE}Done."
```

In case you want to see the progress of a file-copy process, you can simply use

pv source_file > destination_file
or
rsync --progress source_file destination_file
instead of the cp command

....................

This will start an infinite while loop that echoes a spinner every second and is executed in the background.

```bash
while true;do echo -n .;sleep 1;done &
sleep 10 # or do something else here
kill $!; trap 'kill $!' SIGTERM
echo done
```

Instead of using the “sleep 10” command, run any command you want.

When that command finishes executing, this will kill the last job running in the background (which is the infinite while loop)

source: https://stackoverflow.com/a/16348366/1069083

You can use various while loops instead, e.g. a spinner like this:

```bash
while :;do for s in / - \\ \|; do printf "\r$s";sleep 1;done;done
```

https://superuser.com/questions/611538/is-there-a-way-to-display-a-countdown-or-stopwatch-timer-in-a-terminal

```
Explanation of code ---  copy code below SS
#Short answer:

for i in `seq 60 -1 1` ; do echo -ne "\r$i " ; sleep 1 ; done

# Explanation:

# I know there are a lot of answers, but I just want to post something very close to OP's question that I would accept as, indeed, "oneliner countdown in the terminal." My goals were:

#" One-liner Countdown:
# Easy to remember and type in console (no functions and heavy logic, bash only).
It does not require additional software to install (it can be used on any server I go to via SSH, even if I do not have a root there).
#How it works:
"

seq prints numbers from 60 to 1.
echo -ne "\r$i " returns caret to beginning of the string and prints current $i value. Space after it is required to overwrite the previous value if it was longer by characters than the current $ I (10 -> 9).
```

prints out seconds on screen:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/276d21da-de17-4440-8fe7-1fb67fc8ee2a/Untitled.png)

```bash
for i in `seq 60 -1 1` ; do echo -ne "\r$i " ; sleep 1 ; done
```

https://www.google.com/search?q=how+to+one+line+a+timer+function+in+kali+cmd&oq=how+to+one+line+a+timer+function+in+kali+cmd&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRigATIHCAIQIRigAdIBCTE5NDc4ajBqN6gCALACAA&sourceid=chrome&ie=UTF-8

Next experiment 18Jun2024

This will start an infinite while loop that echoes a spinner every second and is executed in the background.

```bash
#worked
while  :;do for s in / - \\ \|; do printf "\r$s";sleep .5;done;done

in `seq 60 -1 1` ; do echo -ne "\r$i " ; sleep 1 ; done

```

- Me:
    
    I'm trying to write a script in my code that waits 5 seconds and does an animation that "spins" until the time is up. 
    

> ChatGPT
> 
> 
> ![ChatGPT.gif](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/d1c430fc-e757-4406-8947-97928361c53a/ChatGPT.gif)
> 

Certainly! Here's your script as a one-liner:

This one-liner will perform the same function: wait for 5 seconds, then display a spinning animation in the terminal.

I see the issue. We must ensure the spinning animation stops once the 5-second wait is complete. Here’s a refined solution:

```bash
# Works!!
(spin() { while :; do for s in / - \\ \|; do printf "\r%s" "$s"; sleep .1; done; done }; spin & pid=$!; sleep 5; kill $pid; printf "\rFunction complete\n")
```

Explanation:

1. `spin()` defines the spinning function.
2. `spin &` starts the spinning animation in the background.
3. `pid=$!` captures the PID of the spinning process.
4. `sleep 5` waits for 5 seconds.
5. `kill $pid` terminates the spinning process.
6. `printf "\rFunction complete\n"` displays the completion message after the spinning stops.

> 
> 

[ChatGPT.ico](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/a13c3c2b-3f69-42d9-9636-7f97d2d7698e/ChatGPT.ico)

Yes, you can create a function that takes a command as an argument and executes it while displaying the spinning animation. Here is how you can do it:

```bash
spinner() {
    local pid
    (
        $1 &
        pid=$!
        spin() { while :; do for s in / - \\ \|; do printf "\r%s" "$s"; sleep .1; done; done }
        spin &
        spin_pid=$!
        wait $pid
        kill $spin_pid
        printf "\rFunction complete\n"
    )
}

# Example usage:
spinner "sleep 5"
```

Explanation:

1. `spinner()` is a function that accepts a command as an argument.
2. The command `$1` is executed in the background, and its PID is captured in `pid`.
3. The `spin()` function is defined to create the spinning animation.
4. `spin &` starts the spinning animation in the background, and its PID is captured in `spin_pid`.
5. `wait $pid` waits for the command to complete.
6. `kill $spin_pid` terminates the spinning animation once the command is done.
7. `printf "\rFunction complete\n"` displays the completion message.

You can use the `spinner` function with any command you want to run while displaying the spinner. For example, you can replace `"sleep 5"` with any other command.

> Me
> 
- I want to create a timer that, when a process starts, I can add in or change later, will time how long that process takes in real-time, and once it is done, will print out the total time the process took
    
    

![ChatGPT.gif](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/d1c430fc-e757-4406-8947-97928361c53a/ChatGPT.gif)

You can use the time command and the spinner animation to create a timer function that times how long a process takes and prints out the total time. Here is a function that does this:

```bash
spinner() {
    (
        start_time=$(date +%s)
        $1 &
        pid=$!
        spin() { while :; do for s in / - \\ \|; do printf "\r%s" "$s"; sleep .1; done; done }
        spin &
        spin_pid=$!
        wait $pid
        end_time=$(date +%s)
        kill $spin_pid
        duration=$((end_time - start_time))
        printf "\rFunction complete\n"
        printf "Total time: %d seconds\n" "$duration"
    )
}

# Example usage:
spinner "sleep 5"

```

Explanation:

1. `spinner()` is a function that accepts a command as an argument.
2. `start_time=$(date +%s)` captures the start time in seconds since the epoch.
3. The command `$1` is executed in the background, and its PID is captured in `pid`.
4. The `spin()` function creates the spinning animation.
5. `spin &` starts the spinning animation in the background, and its PID is captured in `spin_pid`.
6. `wait $pid` waits for the command to complete.
7. `end_time=$(date +%s)` captures the end time in seconds since the epoch.
8. `kill $spin_pid` terminates the spinning animation once the command is done.
9. `duration=$((end_time - start_time))` calculates the total time taken.
10. `printf "\rFunction complete\n"` displays the completion message.
11. `printf "Total time: %d seconds\n" "$duration"` prints the total time the process took.

You can use the `spinner` function with any command, and it will display the spinner animation while timing the process. For example, you can replace `"sleep 5"` with any other command.

SS:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/eb6c5f10-6443-40c9-91ab-8b430b257fed/10c56a90-57dc-4355-96cf-4d26e2413bd2/Untitled.png)
