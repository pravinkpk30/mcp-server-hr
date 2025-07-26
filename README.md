# Leave Management MCP Server

A Model Context Protocol (MCP) server for managing employee leave requests. This server provides a simple API to check leave balances, apply for leave, and view leave history for employees.

## Features

- Check available leave balance for employees
- Apply for leave with specific dates
- View leave history
- Simple in-memory storage (resets on server restart)
- FastAPI-based REST API

## Prerequisites

- Python 3.11 or higher
- UV package manager (recommended) or pip

## Installation

### Build Your First MCP Server: Leave Management
This AI tool helps an HR with leave management related tasks. The codebase here 
is for MCP server that interacts with mock leave database and responds to MCP client queries

### Setup steps
1. Install Claude Desktop
2. Install uv by running `pip install uv`
3. Run `uv init mcp-server-hr` to create a project directory
4. Run `uv add "mcp[cli]"` to add mcp cli in your project
5. Few folks may get type errors for which you can run `pip install --upgrade typer` to upgrade typer library to its latest version
6. Write code in main.py for leave management server
7. Install this server inside Claude desktop by running `uv run mcp install main.py` in the project directory
8. Kill any running instance of Claude from Task Manager. Restart Claude Desktop
9. In Claude desktop, now you will see tools from this server


### Using UV Package Manager (Recommended)

1. Install UV if you haven't already:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. Clone the repository:
   ```bash
   git clone https://github.com/praveenkumar/mcp-server-hr.git
   cd mcp-server-hr
   ```

3. Create and activate a virtual environment:
   ```bash
   uv venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

4. Install dependencies:
   ```bash
   uv pip install -e .
   ```

### Using pip

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -e .
```

## Running the Server

```bash
uvicorn main:app --reload
```

The server will start at `http://127.0.0.1:8000` by default.

## API Endpoints

### 1. Check Leave Balance

**Endpoint:** `GET /get_leave_balance`  
**Parameters:**
- `employee_id` (string, required): Employee ID to check balance for

**Example Request:**
```bash
curl "http://127.0.0.1:8000/get_leave_balance?employee_id=E001"
```

**Example Response:**
```json
"E001 has 18 leave days remaining."
```

### 2. Apply for Leave

**Endpoint:** `POST /apply_leave`  
**Parameters:**
- `employee_id` (string, required): Employee ID
- `leave_dates` (array of strings, required): List of dates in YYYY-MM-DD format

**Example Request:**
```bash
curl -X POST "http://127.0.0.1:8000/apply_leave" \
     -H "Content-Type: application/json" \
     -d '{"employee_id":"E002", "leave_dates":["2025-08-01","2025-08-02"]}'
```

**Example Response:**
```json
"Leave applied for 2 day(s). Remaining balance: 18."
```

### 3. Get Leave History

**Endpoint:** `GET /get_leave_history`  
**Parameters:**
- `employee_id` (string, required): Employee ID

**Example Request:**
```bash
curl "http://127.0.0.1:8000/get_leave_history?employee_id=E001"
```

**Example Response:**
```json
"2024-12-25, 2025-01-01"
```

## Available Employee IDs

- `E001`: Initial balance of 18 days
- `E002`: Initial balance of 20 days

### For Claude Desktop

#### Prerequisites
- Install Claude Desktop from the official Anthropic website
- Python 3.11+ and pip installed

#### Setup Steps
### Install UV Package Manager:
```bash
pip install uv
```
### Initialize a new MCP project:
```bash
uv init my-leave-mcp
cd my-leave-mcp
```
### Install MCP CLI:
```bash
uv add "mcp[cli]"
```
### Install Typer (if needed):
```bash
pip install --upgrade typer
```
### Install the MCP Server:
```bash
mcp install main.py
```
### Restart Claude Desktop:
- Close Claude Desktop completely
- Reopen Claude Desktop
Verification:
- Start a new conversation
- You should see the Leave Management tools available

### For Windsurf

#### Prerequisites
- Windsurf application installed
- MCP server running locally

#### Setup Steps
### Start the MCP Server:
```bash
uvicorn main:app --reload
```
### Configure Windsurf:
- Open Windsurf settings
- Go to "MCP Servers" section
- Click "Add New Server"
- Enter: http://127.0.0.1:8000
- Name it "Leave Management"
- Save the configuration
- Verify Connection:
The Leave Management tools should now be available in Windsurf

#### Common Issues & Solutions

##### Tools Not Appearing
- Ensure you've restarted the application after installation
- Check if the MCP server is running
- Verify the installation command completed successfully

##### Connection Issues
- Confirm the server URL is correct
- Check if the port (default: 8000) is available
- Look for any firewall/network restrictions

##### Type Errors
```bash
pip install --upgrade typer
```

## Development

### Project Structure

- `main.py`: Main application file with all API endpoints
- `pyproject.toml`: Project configuration and dependencies
- `uv.lock`: Lock file for reproducible builds with UV

### Testing

To run tests (if available):

```bash
uv pip install pytest
pytest
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request