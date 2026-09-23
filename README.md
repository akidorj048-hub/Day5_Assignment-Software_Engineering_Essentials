# Day5_Assignment-Software_Engineering_Essentials
Akidor Erot Julias
A) User Manual Procedure: Creating and Activating a Python Virtual Environment
Prerequisites
Before starting, make sure you have:
A Windows computer.
Python installed on the computer.
Git Bash or another terminal such as PowerShell.
Basic knowledge of opening a terminal and entering commands.
An internet connection for installing the package.
Procedure
Step 1
Open Git Bash.
Expected result: A Git Bash terminal window opens.
Step 2
Create a folder named python_setup_lab.
Command:
mkdir python_setup_lab

Expected result: A new folder named python_setup_lab is created.
Step 3
Move into the project folder.
Command:
cd python_setup_lab

Expected result: The terminal is now working inside the python_setup_lab folder.
Step 4
Create a Python virtual environment named venv.
Command:
python -m venv venv

Expected result: A new venv folder is created inside python_setup_lab.
Step 5
Activate the virtual environment.
Command:
source venv/Scripts/activate

Expected result: (venv) appears at the beginning of the terminal prompt.
Step 6
Install the requests package.
Command:
python -m pip install requests

Expected result: Python downloads and installs the requests package and its required dependencies.
Step 7
Display the installed packages.
Command:
python -m pip list

Expected result: A list of installed Python packages appears, including requests.
Step 8
Save the installed packages to a requirements file.
Command:
python -m pip freeze > requirements.txt

Expected result: A file named requirements.txt is created in the python_setup_lab folder.
Screenshot Description
I would include a screenshot showing the Git Bash terminal after running python -m pip list. The screenshot should show (venv) in the terminal prompt and the installed requests package in the package list.
Troubleshooting
Common error: python is not recognized or the virtual environment cannot be created.
This usually means Python is not installed correctly or is not available on the system PATH. Check that Python is installed by running:
python --version

If the command fails, install Python and make sure the option to add Python to the PATH is enabled during installation. Then reopen Git Bash and try the procedure again.
Result
The project now has an isolated Python environment where packages such as requests can be installed without affecting other Python projects.

B) API Reference Entry: Create a New Task
Endpoint
HTTP Method: POST
Endpoint Path:
/projects/{projectId}/tasks

Description
Creates a new task in a specified project for an authenticated user. The request must provide a task title, assignee, due date, and priority. A description may optionally be included.
Path Parameters
Parameter
Type
Required
Description
projectId
integer
Yes
The unique ID of the project where the new task will be created.

Request Body Parameters
Parameter
Type
Required
Description
title
string
Yes
The name or title of the task.
description
string
No
Additional information about the task.
assigneeId
integer
Yes
The unique user ID of the person assigned to the task.
dueDate
string (date)
Yes
The date when the task is due, using YYYY-MM-DD format.
priority
string
Yes
The task priority. Allowed values are low, medium, or high.

Required Request Headers
Header
Required
Description
Authorization
Yes
Contains the user's authentication token in the format Bearer <token>.
Content-Type
Yes
Must be application/json because the request body uses JSON.

Example Request
POST /projects/125/tasks
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

Request Body
{
  "title": "Prepare project presentation",
  "description": "Create the slides and prepare the final presentation.",
  "assigneeId": 42,
  "dueDate": "2026-10-15",
  "priority": "high"
}

Response Codes
201 Created
The task was successfully created.
400 Bad Request
The request contains invalid or missing data, such as an invalid date or an unsupported priority value.
401 Unauthorized
The request does not contain valid authentication credentials.
403 Forbidden
The authenticated user does not have permission to create tasks in the specified project.
404 Not Found
The specified project or assignee does not exist.
409 Conflict
A task cannot be created because it conflicts with an existing resource or project rule.
422 Unprocessable Entity
The request format is valid, but one or more supplied values fail application validation.
500 Internal Server Error
An unexpected error occurred on the server while processing the request.
Example Successful Response
HTTP Status: 201 Created
{
  "id": 987,
  "projectId": 125,
  "title": "Prepare project presentation",
  "description": "Create the slides and prepare the final presentation.",
  "assigneeId": 42,
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "pending",
  "createdAt": "2026-09-23T12:30:00Z"
}

Summary
The POST /projects/{projectId}/tasks endpoint allows an authenticated user to create a new task inside a project. The project ID is supplied in the URL, while the task details are supplied in the JSON request body. A successful request returns 201 Created together with the newly created task's details.

