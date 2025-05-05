Document Conversion APIThis project provides a simple REST API endpoint to convert various document types (DOC, DOCX, XLSX, etc.) to PDF using LibreOffice. It is designed as a reusable component that can be called by other applications.Table of ContentsProject StructurePrerequisitesInstallationConfigurationHow to RunAPI EndpointSwagger UIProject Structuredocument_conversion_api/
├── app.py
├── config.ini
├── requirements.txt
└── static/
    └── swagger.yaml
app.py: The main Flask application file containing the API endpoint and Swagger UI configuration.config.ini: Configuration file for LibreOffice path, temporary folders, and logging.requirements.txt: Lists Python dependencies.static/: Directory to serve static files, including the OpenAPI specification.static/swagger.yaml: The OpenAPI Specification file describing the API for Swagger UI.PrerequisitesPython 3.7+: Ensure Python is installed on your system.pip: Python package installer (usually comes with Python).LibreOffice: LibreOffice must be installed on the machine where this API will run, as the API uses its command-line interface for conversion. Make sure the soffice executable is accessible.InstallationClone or download the project files.Navigate to the project directory in your terminal.(Optional but Recommended) Create a Python virtual environment:python -m venv venv
Activate the virtual environment:On Windows:.\venv\Scripts\activate
On macOS and Linux:source venv/bin/activate
Install the required Python packages:pip install -r requirements.txt
ConfigurationEdit the config.ini file to match your environment:[Logging]
log_file_name = conversion_api.log
log_level = INFO ; DEBUG, INFO, WARNING, ERROR, CRITICAL
log_format = %(asctime)s - %(name)s - %(levelname)s - %(message)s

[FileProcessing]
; Path to LibreOffice executable for document conversion (update this)
libreoffice_path = C:\Program Files\LibreOffice\program\soffice.exe # Example for Windows
; libreoffice_path = /usr/bin/soffice # Example for Linux
; libreoffice_path = /Applications/LibreOffice.app/Contents/MacOS/soffice # Example for macOS
; Base directory for creating temporary folders for conversion tasks
temp_base_folder_name = conversion_temp
libreoffice_path: Crucial - Update this to the actual path of the soffice executable on your system.temp_base_folder_name: The directory where temporary files will be stored during conversion. Ensure the user running the API has write permissions to this location.How to RunEnsure your virtual environment is activated (if used).Navigate to the project directory.Run the Flask application:python app.py
The API will start and listen on the port configured in app.py (default is 5001). You will see output in the terminal indicating the address it's running on.API EndpointPOST /convert-to-pdf: Converts an uploaded document file to PDF.Method: POSTRequest Body: multipart/form-data containing a file with the field name file.Response: Returns the converted PDF file (application/pdf) on success (200 OK) or a JSON object with an error message on failure (400 or 500 status code).Swagger UIAn interactive Swagger UI is available for testing the API directly from your browser.URL: http://<host>:<port>/swagger-ui/By default, if running locally: http://127.0.0.1:5001/swagger-ui/Open this URL in your browser to see the documentation, the /convert-to-pdf endpoint, and use the "Try it out" feature to upload documents for conversion.
