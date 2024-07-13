

# Flask Celery Email Sending Application

This project is a simple Flask application that uses Celery to handle background tasks for sending emails. It demonstrates how to set up a basic Flask app with Celery for asynchronous task processing.

## Features

- Queue email sending tasks using Celery.
- Log email activities.
- View logs of sent emails through a dedicated endpoint.

## Prerequisites

Before you begin, ensure you have the following installed:

- Python 3.6 or higher
- RabbitMQ server
- `pip` package manager

## Getting Started

### Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/yourusername/flask-celery-email-app.git
    cd flask-celery-email-app
    ```

2. **Create a virtual environment and activate it:**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install the required packages:**

    ```bash
    pip install -r requirements.txt
    ```

4. **Set up the `.env` file:**

    Create a `.env` file in the project root directory and add the following environment variables:

    ```env
    EMAIL_USER=your-email@example.com
    EMAIL_PASSWORD=your-email-password
    CELERY_BROKER_URL=pyamqp://guest@localhost//
    CELERY_RESULT_BACKEND=rpc://
    ```

### Running the Application

1. **Start the RabbitMQ server:**

    Ensure RabbitMQ is installed and running on your machine. You can start it using the following command:

    ```bash
    sudo service rabbitmq-server start
    ```

2. **Start the Flask application:**

    ```bash
    python app.py
    ```

3. **Start the Celery worker:**

    Open another terminal, activate the virtual environment, and start the Celery worker:

    ```bash
    celery -A app.celery worker --loglevel=info
    ```

### Usage

#### Queue an Email

To queue an email for sending, use the `/` endpoint with the `sendmail` query parameter:

```http
GET /?sendmail=recipient@example.com
```

#### Log the Current Time

To log the current time, use the `/` endpoint with the `talktome` query parameter:

```http
GET /?talktome
```

#### View Logs

To view the logs of sent emails, use the `/logs` endpoint:

```http
GET /logs
```

### Project Structure

- `app.py`: The main Flask application file with Celery integration and endpoint definitions.
- `.env`: Environment variables for email credentials and Celery configuration (not included in the repository).
- `requirements.txt`: A list of required Python packages.

### Code Explanation

#### Flask and Celery Setup

The Flask application is initialized and configured to use Celery for asynchronous task processing. Celery is configured to use RabbitMQ as the message broker and RPC as the result backend.

#### Logging

The application logs activities such as queuing emails and sending emails to a log file located in the user's home directory.

#### Sending Emails

The `send_email` task is defined to handle sending emails using the SMTP protocol. It uses environment variables for email credentials and SMTP server details.

### Error Handling

Errors encountered during email sending are logged for debugging purposes.

### Security Considerations

- Do not expose your email credentials in the `.env` file if sharing the project.
- Ensure that the log file does not contain sensitive information before sharing or exposing it.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

Make sure to adjust the repository URL in the clone command and other project-specific details as needed. Additionally, create a `requirements.txt` file with the necessary dependencies:

```plaintext
Flask==2.0.2
celery==5.1.2
python-dotenv==0.19.2
```

With this `README.md`, users will have a clear understanding of how to set up, run, and use your Flask Celery email sending application.

These screenshots below show the application deployment using the logs, sendmail and talktome:

![3c59-86-137-237-181 ngrok-free app - Google Chrome 13_07_2024 21_26_40](https://github.com/user-attachments/assets/714a20b3-87c8-4f16-9979-454289df310e)


![3c59-86-137-237-181 ngrok-free app_logs - Google Chrome 13_07_2024 21_27_17](https://github.com/user-attachments/assets/18d1bbee-ca6f-450e-ae6b-c2bb2133256b)


![3c59-86-137-237-181 ngrok-free app__talktome - Google Chrome 13_07_2024 21_28_00](https://github.com/user-attachments/assets/1833f6f5-a9d9-491a-8158-203a79c2e670)


