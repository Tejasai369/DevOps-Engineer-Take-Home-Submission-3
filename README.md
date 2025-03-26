#Implimentation and Scalability

import psutil
import time
import json

LOG_FILE = "monitor.log"

def collect_metrics():
    """Collects system metrics and writes them to a log file."""
    metrics = {
        "timestamp": time.strftime("%Y-%m-%d %H:%M:%S"),
        "cpu_usage": psutil.cpu_percent(interval=1),
        "memory_usage": psutil.virtual_memory().percent,
        "disk_usage": psutil.disk_usage('/').percent
    }

    # Write metrics to log file
    with open(LOG_FILE, "a") as log_file:
        log_file.write(json.dumps(metrics) + "\n")

    print(f"Metrics logged: {metrics}")

if __name__ == "__main__":
    print("Monitoring started... Press Ctrl+C to stop.")
    while True:
        collect_metrics()
        time.sleep(5)  # Collect data every 5 seconds
