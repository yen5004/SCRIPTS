Used when you have a function that needs to call a function from within a script

> me
> 

I have a script that has a function in it; after it runs, I want to be able to run call another function from within the script, how do I tdo that, and show me a simple working example for kali linux

> ChaptGPT
> 

Sure, here's a simple example script in Bash for Kali Linux that demonstrates how to define functions, call a function from another function, and time the execution of a command with a spinner animation.

```bash
#!/bin/bash

# Function to display a spinner animation
spinner() {
    (
        start_time=$(date +%s)
        $1 &
        pid=$!
        spin() { while :; do for s in / - \\ \\|; do printf "\r%s" "$s"; sleep .1; done; done }
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

# Function to simulate a long-running task
long_running_task() {
    echo "Starting long running task..."
    sleep 5
    echo "Long running task completed."
}

# Function to be called after the long-running task
post_task_function() {
    echo "Post task function running..."
}

# Main script
main() {
    # Run the long-running task with a spinner
    spinner long_running_task

    # Call the post task function
    post_task_function
}

# Execute the main function
main

```

Save this script to a file, for example, `script.sh`, and make it executable:

```bash
chmod +x script.sh

```

Run the script:

```bash
./script.sh

```

Explanation:

1. The `spinner` function displays a spinner animation while timing the execution of a command passed as an argument.
2. The `long_running_task` function simulates a long-running task (using `sleep 5`).
3. The `post_task_function` function is called after the long-running task completes.
4. The `main` function runs the `long_running_task` with the spinner and then calls the `post_task_function`.
5. The `main` function is executed at the end of the script.

This script demonstrates how to define and call functions, use a spinner for a long-running task, and call another function after the task completes.

Used when you have a function that needs to call a function from an outside script
