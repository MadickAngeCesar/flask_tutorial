## Run the Application
To run the Flask application in debug mode, use the following command:
```bash
flask --app flaskr run --debug
```

## Initialize the Database File
To initialize the database, run:
```bash
flask --app flaskr init-db
```
This will create a `flaskr.sqlite` file in the instance folder of your project.

## Project Description
The `pyproject.toml` file describes your project and how to build it.

## Build and Install
To deploy your application, build a wheel (`.whl`) file. First, install the `build` tool:
```bash
pip install build
```
Then, build the wheel file:
```bash
python -m build --wheel
```
The wheel file will be located in the `dist` directory, named in the format `{project name}-{version}-{python tag}-{abi tag}-{platform tag}`.

To install the wheel file on another machine, set up a new virtual environment and run:
```bash
pip install flaskr-1.0.0-py3-none-any.whl
```
Since this is a different machine, initialize the database again:
```bash
flask --app flaskr init-db
```
When Flask is installed (not in editable mode), it uses a different directory for the instance folder, located at `.venv/var/flaskr-instance`.

## Configure the Secret Key
In production, change the `SECRET_KEY` to random bytes to ensure security. Use the following command to generate a random secret key:
```bash
python -c 'import secrets; print(secrets.token_hex())'
```
Example output:
```
'192b9bdd22ab9ed4d12e236c78afcb9a393ec15f71bbf5dc987d54727823bcbf'
```
Create a `config.py` file in the instance folder and copy the generated value into it:
```python
SECRET_KEY = '192b9bdd22ab9ed4d12e236c78afcb9a393ec15f71bbf5dc987d54727823bcbf'
```
You can also set other necessary configurations here, although `SECRET_KEY` is the only one required for Flaskr.

## Run with a Production Server
For production, do not use the built-in development server (`flask run`). Instead, use a production WSGI server like Waitress. First, install Waitress:
```bash
pip install waitress
```
Then, run Waitress with the following command:
```bash
waitress-serve --call 'flaskr:create_app'
```
This will serve your application on `http://0.0.0.0:8080`.

For more deployment options, see the Flask documentation on Deploying to Production. Waitress is used in this tutorial because it supports both Windows and Linux, but there are many other WSGI servers and deployment options available.
