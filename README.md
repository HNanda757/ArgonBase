# ArgonBase

The ArgonBase is a lightweight implementation of database management system developed in Java. The system supports a basic SQL-like interface for interacting with the database and demonstrates features like record handling, index creation, and directory management.


Running the code:
1. Download the files
2. Open windows cmd prompt
3. navigate to project directory
4. Then navigate under src folder
5. run the command javac *.java
6. then run the command java ArgonBase.java

OR

1. Download the zip folder to your working directory
2. Open your favorite IDE
3. Run ArgonBase.java


Here’s an in-depth summary of the code in the ArgonBase implementation:

### **ArgonBase.java**  
This is the main driver of the application and acts as the entry point for ArgonBase. It initializes the command-line interface (CLI) for interacting with the database engine. The CLI accepts user inputs in a SQL-like syntax and processes commands until the user exits. The main method sets up the required directories and ensures a functional environment. It uses a `Scanner` to read user commands, and commands are parsed and executed using the functionality defined in other components. This file highlights the modular nature of ArgonBase by delegating actual operations to specialized classes, maintaining a clean separation of concerns.

---

### **Commands.java**  
This file is responsible for parsing and interpreting user commands. It tokenizes the input SQL-like statements and determines the type of command (e.g., `CREATE`, `SELECT`, `SHOW`). Depending on the command type, it invokes specific functions to execute the operations. The file includes methods for handling both metadata operations (like listing tables) and data manipulation commands. It lays the foundation for future expansion, allowing developers to easily add support for new commands or enhance query parsing capabilities.

---

### **Constants.java**  
The `Constants` class contains definitions for various immutable properties used across ArgonBase. These include database-wide settings such as the default page size (512 bytes) and enumerations for different page types (e.g., table interior, table leaf). This centralization of constants ensures consistent usage and simplifies updates to system-wide configurations. The file also provides convenient access methods for enumerations, enabling robust and error-free management of database metadata.

---

### **DatabaseFile.java**  
This is an abstract class that forms the backbone of ArgonBase’s file storage system. It extends `RandomAccessFile` to support direct file manipulation. The class manages the creation and organization of pages within database files, including initialization of empty files with default page headers. It provides functionality to create new pages, manage parent-child relationships, and identify unused pages. By encapsulating common file management tasks, it serves as a base class for `TableFile` and `IndexFile`.

---

### **DataTools.java**  
A utility class providing essential data conversion and manipulation methods, `DataTools` supports operations like converting raw database values to their string representations. It handles various data types (e.g., `YEAR`, `TIME`) and ensures that data conforms to database format specifications. This class is critical for maintaining type safety and consistency when interacting with stored records and their schema definitions.

---

### **Directory.java**  
`Directory` is responsible for setting up the database’s file structure. It ensures that metadata and user data directories are properly initialized. It creates a parent directory for storing all database files and subdirectories for catalogs (metadata) and user data. This class abstracts the complexity of file system operations, making it easier to manage the physical layout of the database. Its error handling ensures robust directory creation even in environments with limited permissions.

---

### **HexDump.java**  
A debugging tool, `HexDump` provides a visual representation of database files in hexadecimal and ASCII formats. It enables developers to inspect the low-level structure of files, including headers, page contents, and data records. This is invaluable for troubleshooting issues with file formatting and for understanding the binary storage model used by ArgonBase.

---

### **IndexFile.java**  
`IndexFile` extends the `DatabaseFile` class and is dedicated to managing database indexes. It creates and maintains index files for specific columns in a table, enabling faster lookups and query execution. The file stores metadata such as the indexed column’s data type and its size, ensuring compatibility with the table’s schema. It also provides methods for accessing indexed data, making it a key component of query optimization.

---

### **Record.java**  
This class represents a single row in a database table. It encapsulates information about the record’s schema, including the data types and values of each column. A `Record` instance includes metadata such as its size and a unique row ID. It also manages the record’s header, which contains information required for efficient storage and retrieval. This class is central to ArgonBase’s data manipulation functionality, providing a clear abstraction of table rows.


### **Settings.java**  
The `Settings` class maintains configuration parameters for ArgonBase, such as directory paths, version information, and runtime state variables. It includes methods for accessing and modifying settings, such as enabling or disabling the exit flag and customizing the command prompt. This class ensures that global settings are easily configurable and consistently applied throughout the system.

---

### **Table.java**  
`Table` is a high-level abstraction of a database table, containing schema information such as column names, data types, and nullability constraints. It interacts with `TableFile` to manage the physical storage of table data and includes metadata for user tables and catalog tables. This class supports operations like creating tables, retrieving schema information, and managing table-specific files. It bridges the gap between logical database concepts and their physical representation.

---

### **TableFile.java**  
An extension of `DatabaseFile`, `TableFile` handles the storage and retrieval of table data. It supports operations like fetching the smallest row ID on a page and determining the type of data stored on a page. This class is tightly integrated with `Table` to ensure seamless management of table-specific operations. It uses the page-based file system to organize records and maintain efficient access patterns.

---

### **Utils.java**  
`Utils` provides auxiliary methods for the ArgonBase system, such as displaying a splash screen and generating formatted output. These utility functions enhance the user experience by providing clear and consistent messages. The splash screen, for instance, is displayed when the application starts, welcoming users and providing essential information about the system.
