# DevOps Dashboard Application

This is a simple Flask application providing a basic DevOps dashboard with health check and statistics endpoints.

## Overview

The application provides the following functionalities:

-   **Homepage (`/`):** Displays a welcome message, service status, server time, and the number of requests served.
-   **Health Check (`/health`):** Returns a JSON response with the application's health status, timestamp, uptime, and the number of requests served.
-   **Statistics (`/stats`):** Returns a JSON response containing service statistics such as the total number of requests, current time, hostname, environment, and a message.
-   **Custom 404 Handler:** Returns a JSON response with an error message when an invalid endpoint is accessed.

## Requirements

-   Python 3.6+
-   Flask (version specified in `requirements.txt`)

## Installation

1.  Clone the repository:

    ```bash
    git clone <repository_url>
    cd <repository_directory>
    ```

2.  Create a virtual environment (recommended):

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Linux/macOS
    venv\Scripts\activate  # On Windows
    ```

3.  Install the dependencies:

    ```bash
    pip install -r requirements.txt
    ```

## Running the Application

To run the application, execute the following command:

```bash
python app.py