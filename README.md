### 🖥️ System Activity Log
```bash
### Phase 2: The Script (`update_log.py`)

Create a file in your repo named `update_log.py`. This script fetches your public events and formats them.

```python
import requests
import datetime
import os
import re

# Your GitHub Username
USERNAME = "YOUR_USERNAME_HERE"

def fetch_activity():
    url = f"https://api.github.com/users/{USERNAME}/events/public"
    response = requests.get(url)
    if response.status_code != 200:
        return []
    return response.json()

def format_log(event):
    # Format timestamp to look like a server log
    created_at = event['created_at']
    dt = datetime.datetime.strptime(created_at, "%Y-%m-%dT%H:%M:%SZ")
    timestamp = dt.strftime("%Y-%m-%d %H:%M:%S")

    repo_name = event['repo']['name']
    event_type = event['type']
    
    # Custom Log Levels based on event type
    if event_type == "PushEvent":
        log_level = "[INFO]"
        commit_msg = event['payload']['commits'][0]['message'].split('\n')[0]
        # Truncate long messages
        if len(commit_msg) > 40: commit_msg = commit_msg[:40] + "..."
        message = f"Pushed to {repo_name}: \"{commit_msg}\""
    elif event_type == "PullRequestEvent":
        action = event['payload']['action']
        log_level = "[SUCCESS]" if action == "closed" else "[WARN]"
        message = f"PR {action} in {repo_name}"
    elif event_type == "CreateEvent":
        log_level = "[SYSTEM]"
        ref_type = event['payload']['ref_type']
        message = f"Created new {ref_type} in {repo_name}"
    else:
        return None # Skip other events to keep it clean

    return f"{log_level}  {timestamp}  {message}"

def update_readme(logs):
    # Join the last 5 logs
    log_content = "\n".join(logs[:5])
    
    with open("README.md", "r") as file:
        readme = file.read()

    # Regex to find the block between the tags
    pattern = r"(.*?)"
    replacement = f"\n{log_content}\n"
    
    new_readme = re.sub(pattern, replacement, readme, flags=re.DOTALL)

    with open("README.md", "w") as file:
        file.write(new_readme)

if __name__ == "__main__":
    events = fetch_activity()
    formatted_logs = []
    
    for event in events:
        log = format_log(event)
        if log:
            formatted_logs.append(log)
            
    if formatted_logs:
        update_readme(formatted_logs)
