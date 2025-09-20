# 🤖 Text-to-SQL by A2A Protocol

This project demonstrates an **Agent-to-Agent (A2A) protocol** that converts natural language queries into **SQL statements**, executes them on a database, and returns meaningful results. It uses a modular, agent-based architecture for flexibility and scalability.

## 🚀 Features

- **Natural Language Processing** - Convert natural language text into SQL queries
- **Modular Agent Architecture**:
  - `TextToSQLAgent` → Generates SQL queries from natural language
  - `SQLExecutionAgent` → Executes SQL queries on the database
- **Built-in Hospital Patients Database** - Sample SQLite database (`hospital_patients.db`) for testing
- **Protocol-driven Communication** - Uses MCP (Multi-agent Communication Protocol) for agent interaction
- **Extensible Design** - Easy to add custom agents or integrate new databases
- **Real-time Query Execution** - Instant results with formatted output

## 🏗️ Architecture

The system uses an **Agent-to-Agent (A2A) protocol** where specialized agents communicate to process user requests:

```
User Input → TextToSQLAgent → SQLExecutionAgent → Formatted Results
```

Each agent has specific responsibilities, making the system modular and maintainable.

## 📂 Project Structure

```
project/
├── Main_Bot.py                   # Entry point for running the bot
├── MCP_Protocol.py              # Defines the A2A protocol
├── agent_card.py                # Agent metadata and configuration
├── agent_registry.py            # Agent management/registration
├── create_DB.py                 # Script to create the sample database
├── show_datas.py               # Utility to display database contents
├── Agents/
│   ├── Text_to_Sql_Agent.py    # Converts text to SQL queries
│   └── SQL_execution_agent.py   # Executes SQL queries
├── requirements.txt             # Python dependencies
└── hospital_patients.db        # Example SQLite database
```

## ⚙️ Installation

### 1. Clone the repository
```bash
git clone https://github.com/Sham1616/Text-to-SQL-by-A2A-Protocol.git
cd Text-to-SQL-by-A2A-Protocol/project
```

### 2. Create a virtual environment (recommended)
```bash
python -m venv venv

# On Windows
venv\Scripts\activate

# On Linux/Mac
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. (Optional) Recreate the database
```bash
python create_DB.py
```

### 5. Verify installation
```bash
python show_datas.py  # View sample database contents
```

## ▶️ Usage

### Start the application
```bash
python Main_Bot.py
```

### Example interactions

```bash
Input: "Show me all patients older than 60"
Output: 
+----+----------+-----+---------+
| ID | Name     | Age | Disease |
+----+----------+-----+---------+
|  3 | John Doe |  65 | Diabetes|
+----+----------+-----+---------+

Input: "Count patients with heart disease"
Output: 
Total patients with heart disease: 5

Input: "Find the average age of patients"
Output:
Average age: 42.3 years
```

## 🤖 Agents Overview

### TextToSQLAgent
- **Purpose**: Parses natural language queries and generates corresponding SQL statements
- **Capabilities**: 
  - Understanding complex query structures
  - Handling aggregations (COUNT, AVG, SUM)
  - Processing filtering conditions
  - Table and column name mapping

### SQLExecutionAgent
- **Purpose**: Executes SQL queries safely and returns formatted results
- **Capabilities**:
  - Query validation and sanitization
  - Result formatting and presentation
  - Error handling and reporting
  - Connection management

### Agent Registry
- **Purpose**: Manages agent lifecycle and capabilities
- **Features**:
  - Agent discovery and registration
  - Capability matching
  - Load balancing (future enhancement)

## 📊 Sample Database Schema

The included `hospital_patients.db` contains:

```sql
CREATE TABLE patients (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER NOT NULL,
    disease TEXT NOT NULL,
    admission_date DATE,
    doctor TEXT
);
```

## 📖 Example Queries

Try these natural language queries:

- **Basic Queries**
  - "Show patients younger than 30"
  - "Find all patients treated by Dr. Smith"
  
- **Aggregation Queries**
  - "Count how many patients have heart disease"
  - "What's the average age of patients?"
  - "Show the oldest patient"

- **Complex Queries**
  - "List patients admitted this month with chronic conditions"
  - "Find patients over 50 with diabetes or heart disease"
  - "Show the distribution of diseases by age group"
 
Sample Outputs:
Screenshots:

<img width="1919" height="966" alt="Screenshot 2025-09-20 103316" src="https://github.com/user-attachments/assets/251599ec-a60d-48f6-96dc-ba6c95af4fd6" />
<img width="940" height="610" alt="image" src="https://github.com/user-attachments/assets/e2ed29dc-118c-43a9-ac12-464862ebeb60" />


## 📦 Dependencies

- **Python 3.9+** (Required)
- **sqlite3** (Built-in with Python)
- **Additional libraries** (see `requirements.txt`):
      transformers
      torch
      pandas
      sqlalchemy
      datasets
      scikit-learn
      tqdm
      numpy


Install all dependencies:
```bash
pip install -r requirements.txt
```

## 🔧 Configuration

### Database Configuration
Modify database settings in `MCP_Protocol.py`:
```python
DATABASE_PATH = "hospital_patients.db"
```

### Agent Configuration
Agent settings can be modified in `agent_card.py`:
```python
AGENT_CONFIG = {
    "text_to_sql": {
        "model": "gpt-3.5-turbo",  # or your preferred model
        "temperature": 0.1
    }
}
```

## 🚀 Extending the System

### Adding New Agents
1. Create a new agent class in the `Agents/` directory
2. Register the agent in `agent_registry.py`
3. Update the protocol in `MCP_Protocol.py`

### Adding New Databases
1. Create your database schema
2. Update the agent configurations
3. Add schema information to the TextToSQLAgent

### Example: Adding a New Agent
```python
class CustomAnalysisAgent:
    def __init__(self):
        self.name = "CustomAnalysisAgent"
        self.capabilities = ["data_analysis", "visualization"]
    
    def process(self, request):
        # Your custom logic here
        return response
```

## 🧪 Testing

Run the test suite:
```bash
python -m pytest tests/  # If tests are implemented
```

Manual testing with sample queries:
```bash
python Main_Bot.py
# Try the example queries listed above
```

## 🐛 Troubleshooting

### Common Issues

**Database not found error**
```bash
python create_DB.py  # Recreate the database
```

**Import errors**
```bash
pip install -r requirements.txt  # Reinstall dependencies
```

**SQL parsing errors**
- Check your natural language query syntax
- Try simpler queries first
- Verify table and column names

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Thanks to the open-source community for the amazing libraries
- Inspired by modern agent-based architectures
- Built with ❤️ for the developer community

