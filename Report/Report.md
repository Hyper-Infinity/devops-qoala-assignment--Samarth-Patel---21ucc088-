# Debugging Assignment Report

## Issues Identified

1. **Missing HTML Directory**:
   - **Description**: The `nginx/Dockerfile` included the command `COPY ./html /usr/share/nginx/html`, but no `html` directory was present in the project structure.
   - **Impact**: This caused the Docker build to fail since it was trying to copy a nonexistent directory.

2. **MAC Address Retrieval Issue**:
   - **Description**: During application testing, the function to retrieve the MAC address of the host returned `00:00:00:00:00:00` for some interfaces. This address is generally invalid and unhelpful for identifying the host.
   - **Impact**: Displaying `00:00:00:00:00:00` as the MAC address would not provide useful information to end users.

## Resolution Steps

1. **Resolution for Missing HTML Directory**:
   - **Action Taken**: To resolve the missing `html` directory issue, I removed or commented out the line `COPY ./html /usr/share/nginx/html` in the `nginx/Dockerfile`. Alternatively, I could have created an empty `html` folder if the application required serving static files. This allowed the Docker image to build successfully without errors related to missing directories.

2. **Resolution for MAC Address Retrieval Issue**:
   - **Action Taken**: I modified the `get_mac_address()` function in `app.py` to skip any MAC address that was equal to `00:00:00:00:00:00`. The updated function checks if the retrieved MAC address is valid (i.e., not `00:00:00:00:00:00`) before returning it. This ensured that the application would only display meaningful MAC addresses or `"N/A"` if none were found.

---