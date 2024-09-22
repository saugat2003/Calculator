---

# Django Calculator Application

A simple calculator web application built using Django and jQuery. This project demonstrates how to build a basic Django app with dynamic calculation functionality using JavaScript and AJAX.

## Features

- Basic arithmetic operations: addition, subtraction, multiplication, and division.
- Responsive calculator interface.
- Securely handles user input using server-side validation to prevent code injection.
- AJAX-based calculation (no page reload).
- Clean and modern UI with HTML, CSS, and JavaScript.

## Project Structure

```
calculator/
│
├── calculator_app/
│   ├── static/
│   │   └── calculator/
│   │       └── style.css         # Styles for the calculator
│   ├── templates/
│   │   └── calculator/
│   │       └── index.html        # HTML template for the calculator
│   ├── views.py                  # Views for handling requests
│   ├── urls.py                   # URL routing for the app
│   └── __init__.py
│
├── manage.py                     # Django management script
├── requirements.txt              # Python dependencies
└── settings.py                   # Project settings
```

## Prerequisites

Before running the project, ensure you have the following installed:

- [Python 3.x](https://www.python.org/)
- [Django 5.x](https://www.djangoproject.com/) (or latest compatible version)
- Pip for Python package management

## Setup Instructions

1. **Clone the repository:**

   ```bash
   git clone https://github.com/saugat2003/Calculator.git
   cd Calculator
   ```

2. **Set up a virtual environment (Recommended):**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**

   Install the required Python packages from `requirements.txt`:

   ```bash
   pip install -r requirements.txt
   ```

   If `requirements.txt` is not available, manually install Django:

   ```bash
   pip install django
   ```

4. **Run database migrations (even if this project doesn't use the database much):**

   ```bash
   python manage.py migrate
   ```

5. **Run the Django development server:**

   ```bash
   python manage.py runserver
   ```

6. **Access the application:**

   Open your browser and go to `http://127.0.0.1:8000/` to use the calculator.

## Usage

1. Once the server is running, navigate to the main calculator page.
2. Enter numbers and operations (`+`, `-`, `*`, `/`) using the on-screen buttons.
3. Click `=` to perform the calculation, which will be processed via an AJAX request to the server.
4. The result will be displayed on the calculator screen without reloading the page.

## Project Configuration

- **Static Files:**
  The project's static files (like CSS) are stored in `calculator_app/static/calculator/`. The file `style.css` provides basic styling for the calculator interface.
  
  In `settings.py`, static files are configured with the following settings:

  ```python
  STATIC_URL = '/static/'
  STATICFILES_DIRS = [BASE_DIR / 'calculator' / 'static']
  ```

- **AJAX Functionality:**
  The app uses jQuery to handle AJAX requests for performing calculations. The calculation request is sent to the Django backend and the result is returned without reloading the page.

## Code Overview

- **Views (`views.py`)**: Contains two views:
  - `index(request)`: Renders the calculator's main page.
  - `calculate(request)`: Processes the user input sent via AJAX, performs the calculation, and returns the result as a JSON response.

- **HTML (`index.html`)**: The front-end of the application, including the calculator interface and JavaScript to handle user input and AJAX requests.

- **CSS (`style.css`)**: Styles the calculator, making it responsive and visually appealing.

### Example JavaScript for AJAX:

```javascript
function calculate() {
    let expression = document.getElementById('display').value;

    // AJAX POST request to Django's calculate view
    $.post('/calculate/', {'expression': expression}, function(data) {
        if (data.error) {
            document.getElementById('display').value = data.error;
        } else {
            document.getElementById('display').value = data.result;
        }
    });
}
```

### Security Note:
- The `calculate()` view uses Python's `eval()` function to evaluate expressions. While this is fine for learning purposes, **do not use `eval()` in production** as it can be vulnerable to code injection attacks. You should use a safer alternative for evaluating mathematical expressions.

## Contributing

If you find any bugs or want to contribute to improving the project, feel free to submit a pull request or open an issue.

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
