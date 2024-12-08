# Log File Analysis Script

This Python script performs various log file analysis tasks. It processes a web server log file to generate insights such as the number of requests by IP address, the most frequently accessed endpoint, and any suspicious activity (e.g., failed login attempts).

## Features

1. **Count Requests by IP Address**:
   - Counts how many requests each IP address has made to the server.
   - Sorts the IPs based on the number of requests, displaying the most active IPs.

2. **Identify the Most Frequently Accessed Endpoint**:
   - Analyzes the log to find the most frequently accessed endpoint (e.g., `/login`, `/home`, etc.).

3. **Detect Suspicious Activity**:
   - Detects suspicious activity by identifying IP addresses that have made more than a specified number of failed login attempts (default is 10). This is useful for spotting potential brute-force attacks.

4. **Save Results to CSV**:
   - Saves the analysis results to a CSV file for easy viewing and further processing.

## Requirements

- Python 3.x
- `re` (regular expressions module, which is part of Python's standard library)
- `collections.Counter` (part of Python's standard library)
- `csv` (part of Python's standard library)

## Usage

1. **Prepare your log file**: Ensure that your log file is in a readable format and contains IP addresses and endpoints that the script can parse. The script assumes that each line contains an IP address and information about requests (e.g., status codes or credentials).

2. **Modify `log_file_path`**: In the script, replace `'example.log'` with the path to your actual log file.

3. **Run the Script**:
   - After setting the correct log file path, run the script. It will:
     - Print the number of requests per IP address.
     - Print the most frequently accessed endpoint.
     - Print any suspicious activity (failed login attempts exceeding the threshold).
     - Save the analysis results to `log_analysis_results.csv`.

4. **Check the Output**:
   - The results are saved in a CSV file named `log_analysis_results.csv` by default. You can open this file in a spreadsheet editor to view the results.

## Functions

### `count_requests_by_ip(log_file_path)`
- **Purpose**: Counts requests by each IP address.
- **Parameters**: `log_file_path` (str) - Path to the log file.
- **Returns**: A list of tuples with IP addresses and their respective request counts, sorted by count.

### `most_frequent_endpoint(log_file_path)`
- **Purpose**: Finds the most frequently accessed endpoint.
- **Parameters**: `log_file_path` (str) - Path to the log file.
- **Returns**: A tuple with the most accessed endpoint and its access count.

### `detect_suspicious_activity(log_file_path, threshold=10)`
- **Purpose**: Detects suspicious activity based on failed login attempts.
- **Parameters**:
  - `log_file_path` (str) - Path to the log file.
  - `threshold` (int) - The number of failed login attempts before an IP is considered suspicious. Default is 10.
- **Returns**: A dictionary of IPs with failed login attempts exceeding the threshold.

### `save_results_to_csv(requests_by_ip, most_accessed_endpoint, suspicious_activity, output_file="log_analysis_results.csv")`
- **Purpose**: Saves the analysis results to a CSV file.
- **Parameters**:
  - `requests_by_ip` (list) - The result of `count_requests_by_ip`.
  - `most_accessed_endpoint` (tuple) - The result of `most_frequent_endpoint`.
  - `suspicious_activity` (dict) - The result of `detect_suspicious_activity`.
  - `output_file` (str) - The output CSV file name. Default is `log_analysis_results.csv`.

## Example

```python
log_file_path = 'example.log'  # Replace this with your log file path
requests_by_ip = count_requests_by_ip(log_file_path)
most_accessed_endpoint = most_frequent_endpoint(log_file_path)
suspicious_activity = detect_suspicious_activity(log_file_path)
save_results_to_csv(requests_by_ip, most_accessed_endpoint, suspicious_activity)
