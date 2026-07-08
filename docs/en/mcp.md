# MyBatis MCP (Model Context Protocol) Support

MyBatisCodeHelper-Pro provides **MCP (Model Context Protocol)** support, enabling AI coding assistants (such as Claude Code) to interact directly with your MyBatis project, making MyBatis development faster, more accurate, and more context-efficient.

---

# 🚀 Why Use MyBatis MCP?

When working with MyBatis projects, AI coding assistants frequently need to:

* Locate the XML file corresponding to a mapper interface
* Inspect database table schemas
* Discover existing SQL statements

Without MCP, the AI typically searches the project, opens XML files, and extracts the required information itself. Besides consuming additional tokens, this also fills the conversation context with large amounts of XML that are irrelevant to the final answer.

## With MCP vs. Without MCP

| Operation                            | Without MCP                                               | With MCP                                  |                  Typical Savings                  |
| ------------------------------------ | --------------------------------------------------------- | ----------------------------------------- | :-----------------------------------------------: |
| Find mapper → XML mapping            | Search project files and verify mapping (~150–250 tokens) | **Single MCP call (~30–60 tokens)**       |                **~100–200 tokens**                |
| List SQL statements                  | Read XML file (~1,000–2,500 tokens depending on size)     | **Returns structured statement metadata** |              **~1,000–2,500 tokens**              |
| Query table columns                  | Read DDL or inspect database (~300–500 tokens)            | **Single MCP call (~50 tokens)**          |                **~250–450 tokens**                |
| Typical MyBatis development workflow | Multiple searches, XML reads, schema lookups              | **Direct MCP queries**                    | **Typically 60–90% less MyBatis-related context** |

> Locating a mapper XML saves only a small number of tokens. The larger savings come from avoiding large XML reads and schema lookups. During real development these operations are often combined, so the overall savings accumulate quickly.

---

# 📉 Cleaner Conversation Context

Without MCP, AI assistants often need to load entire XML files into the current conversation context.

For example, if a conversation involves three different mappers:

```text
Without MCP:
3 × ~2,000 tokens
≈ 6,000 tokens of XML occupying the current conversation context

With MCP:
3 × ~50 tokens
≈ 150 tokens of structured metadata
```

That's roughly **5,800 fewer tokens** occupying the context window.

A cleaner context allows the model to focus on the information that actually matters instead of large XML documents, often resulting in faster and more accurate responses.

---

# 📈 Larger Projects Benefit Even More

| Project Size | Typical XML Size |     XML Read Cost    | Working with 5 Mappers |
| ------------ | :--------------: | :------------------: | :--------------------: |
| Small        |      5–10 KB     |  ~1,000–2,500 tokens |  ~5,000–12,500 tokens  |
| Medium       |     15–30 KB     |  ~4,000–7,500 tokens |  ~20,000–37,500 tokens |
| Large        |     30–50 KB     | ~7,500–12,500 tokens |  ~37,500–62,500 tokens |

As projects grow, mapper XML files become larger and more numerous. MCP continues to return only the information the AI actually needs, making its advantages increasingly significant.

---

# 🛠️ Available MCP Tools

## `find_mapper_xml`

Find the XML file corresponding to a Java mapper interface.

**Input**

* Fully qualified mapper class name
* `.java` file path

**Output**

* Matching mapper XML file path(s)

```text
Input:
com.example.mapper.UserMapper

Output:
src/main/resources/mapper/UserMapper.xml
```

> Large projects often contain multiple XML files with identical names under different directories (for example, `mapper/` and `easycode/`). IDE-based indexing allows MCP to locate the correct mapping much more reliably than file searching alone.

---

## `find_mapper_interface`

Find the Java mapper interface corresponding to an XML file.

**Input**

* XML file path

**Output**

* Namespace
* Java interface path

```text
Input:
src/main/resources/mapper/UserMapper.xml

Output:
com.example.mapper.UserMapper
```

---

## `get_table_columns`

Retrieve database table columns.

**Input**

* Table name

**Output**

* Column names
* Corresponding Java types

```text
user

id          → Long
username    → String
email       → String
create_time → Date
```

> The AI can retrieve table metadata directly through MCP without manually opening a database client or inspecting DDL.

---

## `list_mapper_statements`

List SQL statements defined in a mapper.

**Input**

* Mapper interface (FQN or `.java` path)
* XML file path

**Output**

* Statement ID
* Statement type
* Line number

```text
selectByPrimaryKey   → select (line 28)
insert               → insert (line 40)
updateByPrimaryKey   → update (line 145)
deleteByPrimaryKey   → delete (line 35)
```

> Quickly discover available SQL statements without reading hundreds of lines of XML.

---

## `list_data_sources`

List project data sources.

**Output**

* Data source name
* Database type
* JDBC URL

---

# 📦 Configuration

Add the following configuration to your MCP-compatible AI coding assistant (for example, Claude Code):

```json
{
  "mcpServers": {
    "mybatisMcp": {
      "type": "intellij",
      "name": "MyBatis MCP",
      "description": "MyBatis MCP support — mapper lookup, SQL discovery and schema inspection",
      "tools": [
        "find_mapper_xml",
        "find_mapper_interface",
        "get_table_columns",
        "list_mapper_statements",
        "list_data_sources"
      ]
    }
  }
}
```

> This is an example configuration. The MCP server is provided by the **MyBatisCodeHelper-Pro** IntelliJ IDEA plugin.

---

# 🚦 Starting the MCP Server

The MCP server is started manually inside IntelliJ IDEA.

## Method 1 (Recommended)

```text
Tools
    └── MyBatisCodeHelper
            └── Start MCP Server
```

A notification will appear in the IDE once the server has started.

---

## Method 2

```text
Settings / Preferences

Tools
    └── MyBatisCodeHelper
            └── MCP Server
                    └── Start
```

---

## Verify the Server Is Running

After startup, the menu item changes from

```text
Start MCP Server
```

to

```text
Stop MCP Server
```

indicating that the server is running and available to your AI coding assistant.

> The MCP server is available only while IntelliJ IDEA is running. Restart the server after reopening the IDE.

---

# 💡 Recommended Use Cases

| Scenario                           | MCP Tool                 |
| ---------------------------------- | ------------------------ |
| Locate a mapper XML                | `find_mapper_xml`        |
| Find the Java interface from XML   | `find_mapper_interface`  |
| Inspect a table before writing SQL | `get_table_columns`      |
| Discover existing SQL statements   | `list_mapper_statements` |
| View configured data sources       | `list_data_sources`      |

---

# 📊 Key Benefits

1. **🎯 More Accurate** — Uses IntelliJ IDEA indexing and MyBatis metadata to locate mapper resources more reliably.
2. **📉 Smaller Context** — Returns structured metadata instead of entire XML files, reducing unnecessary context usage.
3. **⚡ Faster Responses** — Eliminates repeated file searches and XML parsing.
4. **💰 Lower Token Consumption** — Reduces unnecessary XML and schema reads during MyBatis development.
5. **📈 Better Scalability** — The larger your project, the greater the benefits of structured access through MCP.
