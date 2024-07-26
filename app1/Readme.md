
```markdown
# Rule Engine Application with AST


## Features

- **Create Rule:** Build complex rules and represent them as AST.
- **Combine Rules:** Merge multiple rules into a single AST.
- **Evaluate Rule:** Test data against rules to determine if conditions are met.
- **Simple UI:** Interact with the rule engine through a web interface.
- **Persistence:** Store rules in a SQLite database for reuse and modification.

## Technology Stack

- **Frontend:** HTML/CSS/JavaScript
- **Backend:** Python/Flask
- **Database:** SQLite

## Installation

### Prerequisites

- Python 3.x installed on your system.
- Pip (Python package manager) installed.

### Setup Instructions

1. **Clone the repository:**

   ```bash
   git clone [repository-link]
   cd rule-engine
   ```

2. **Create a virtual environment:**

   ```bash
   python -m venv venv
   ```

3. **Activate the virtual environment:**

   - On Windows:

     ```bash
     venv\Scripts\activate
     ```

   - On macOS/Linux:

     ```bash
     source venv/bin/activate
     ```

4. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

5. **Set up the database:**

   The application will automatically create the SQLite database and necessary tables on the first run.

6. **Run the application:**

   ```bash
   python app.py
   ```

7. **Access the application:**

   - Open your browser and go to `http://localhost:5000` to access the UI.

## Application Structure

- **`app.py`**: Main application file containing the Flask server and API endpoints.
- **`helper.py`**: Contains logic for creating and evaluating the AST.
- **`templates/`**: Contains HTML templates for the web UI.

## API Endpoints

1. **Create Rule:**

   - **Endpoint:** `/create_rule`
   - **Method:** POST
   - **Request Body:**

     ```json
     {
       "rule_string": "(age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')"
     }
     ```

   - **Response:**

     ```json
     {
       "id": 1,
       "rule_string": "...",
       "ast_json": "..."
     }
     ```

2. **Combine Rules:**

   - **Endpoint:** `/combine_rules`
   - **Method:** POST
   - **Request Body:**

     ```json
     {
       "rule_ids": [1, 2]
     }
     ```

   - **Response:**

     ```json
     {
       "combined_ast_json": "..."
     }
     ```

3. **Evaluate Rule:**

   - **Endpoint:** `/evaluate_rule`
   - **Method:** POST
   - **Request Body:**

     ```json
     {
       "ast_json": "...",
       "data": {
         "age": 35,
         "department": "Sales",
         "salary": 60000,
         "experience": 3
       }
     }
     ```

   - **Response:**

     ```json
     {
       "result": true
     }
     ```

## Database Schema

The SQLite database consists of a single table:

```sql
CREATE TABLE rules (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    rule_string TEXT NOT NULL,
    ast_json TEXT NOT NULL
);
```

## Deployment

For production deployment, consider using a production-ready server like Gunicorn and a reverse proxy like Nginx. Here’s a basic guide for deploying with Gunicorn:

1. **Install Gunicorn:**

   ```bash
   pip install gunicorn
   ```

2. **Run the application with Gunicorn:**

   ```bash
   gunicorn app:app
   ```

3. **Configure Nginx as a reverse proxy:** (Optional, for production environments)

   Create an Nginx configuration file to proxy requests to the Gunicorn server.

## Testing

To test the application, you can use tools like Postman or cURL to interact with the API endpoints. Additionally, the provided UI allows for rule creation, combination, and evaluation.

## Future Enhancements

- Add support for more complex logical expressions.
- Implement user authentication and authorization.
- Extend the UI for enhanced user experience.
- Add error handling for invalid inputs.

