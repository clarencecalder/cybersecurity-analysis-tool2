# cybersecurity-analysis-tool2
import re

def analyze_log(file_path):
    suspicious_patterns = [
        "failed password",
        "invalid user",
        "authentication failure",
        "denied",
        "error",
    ]

    ip_regex = r"(\d{1,3}\.){3}\d{1,3}"
    incidents = []

    with open(file_path, "r", errors="ignore") as log:
        for line in log:
            lower = line.lower()

            for pattern in suspicious_patterns:
                if pattern in lower:
                    ip_match = re.search(ip_regex, line)
                    ip = ip_match.group(0) if ip_match else "unknown"

                    incidents.append((pattern, ip, line.strip()))
                    break

    print("\n=== Log Analysis
