# network_bandwith_monitor
This Python program monitors network bandwidth usage and displays real-time statistics, including upload and download speeds.

Code explained ~ 
```
# Import the psutil library for system and network monitoring
import psutil

# Import the time module for introducing delays
import time

# Define a function to get the total bytes sent and received
def get_bytes_sent_received():
    """
    Get the total bytes sent and received.
    """
    # Use psutil to retrieve network I/O statistics
    net_io = psutil.net_io_counters()

    # Extract the number of bytes sent and received
    bytes_sent = net_io.bytes_sent
    bytes_received = net_io.bytes_recv

    # Return the bytes sent and received
    return bytes_sent, bytes_received

# Define a function to calculate upload and download speeds
def calculate_speed(prev_sent, prev_received, interval):
    """
    Calculate upload and download speeds in bytes per second (B/s).
    """
    # Get the current bytes sent and received
    current_sent, current_received = get_bytes_sent_received()

    # Calculate the upload and download speeds in B/s
    sent_speed = (current_sent - prev_sent) / interval
    received_speed = (current_received - prev_received) / interval

    # Return the calculated speeds
    return sent_speed, received_speed

# Define the main function
def main():
    try:
        # Set the update interval for monitoring in seconds
        interval = 1

        # Initialize the previous bytes sent and received
        prev_sent, prev_received = get_bytes_sent_received()

        # Enter a continuous monitoring loop
        while True:
            # Calculate upload and download speeds
            sent_speed, received_speed = calculate_speed(prev_sent, prev_received, interval)

            # Update the previous bytes sent and received
            prev_sent, prev_received = get_bytes_sent_received()

            # Print upload and download speeds with formatting
            print(f"Upload speed: {sent_speed:.2f} B/s")
            print(f"Download speed: {received_speed:.2f} B/s")

            # Print a separator line
            print("-" * 30)

            # Pause for the specified interval
            time.sleep(interval)

    except KeyboardInterrupt:
        # Handle keyboard interruption and print a message
        print("\nMonitoring stopped.")

# Execute the main function if the script is run directly
if __name__ == "__main__":
    main()

```
output :

![output](https://github.com/Zorgod-x/network_bandwith_monitor/assets/99272119/5b2a9697-62b5-43d4-898b-26f6007ba371)
