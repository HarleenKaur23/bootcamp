### Assignment: Trade File Parsing and Database Insertion**

**Objective**: Write a Java program that reads trade data from a file and inserts it into a database. Use JDBC `PreparedStatement` for database insertion, and implement batch processing for efficiency. The program should handle errors during file parsing and insertion and throw a custom exception if errors exceed a specified threshold.

#### **Requirements**:

1. **File Input**:
   
   - The trade data file will be in a CSV format with the following columns:
     - `trade_id` (String)
     - `trade_identifier` (String) 
     - `ticker_symbol` (String)
     - `quantity` (Integer)
     - `price` (Decimal)
     - `trade_date` (Date in `yyyy-MM-dd` format)
   - The file path will be provided by the user at runtime.
   
2. **Database Structure**:
   - Create a database table named `Trades` with columns matching the fields in the CSV file:
     ```sql
     CREATE TABLE Trades (
         trade_id VARCHAR(20) PRIMARY KEY,
         trade_identifier VARCHAR(20),
         ticker_symbol VARCHAR(10),
         quantity INT,
         price DECIMAL(15, 2),
         trade_date DATE
     );
     ```
   
3. **Implementation Details**:
   - Use `PreparedStatement` to insert data into the `Trades` table.
   - Use JDBC batching to batch the insert operations for improved performance.
   - If more than **25%** of the rows in the file contain errors (e.g., missing data, incorrect data types), throw a custom exception `HitErrorsThresholdException`. this is for the case where file record read fails. 
   - If the record insert fails for that threshold then throw `HitInsertErrorsThresholdException` (`executeBatch` returns the count for rows that were inserted successfully, keep account of that)
   - Properly handle exceptions and rollback the transaction if an error occurs during batch execution.
   - Provide detailed error messages for any row that fails to parse or insert into the database.
   
4. **Custom Exception**:
   - Create a custom exception class named `HitErrorsThresholdException`. This exception will be thrown if the program detects that more than **25%** of the rows in the file contain errors.

5. **Steps**:
   - Prompt the user for the file path.
   - Read the file line by line and validate the data:
     - Ensure all fields are present.
     - Validate data types (e.g., integer for `quantity`, decimal for `price`, and proper date format for `trade_date`).
   - Use a `PreparedStatement` for inserting rows into the `Trades` table.
   - Add each valid row to a batch. If a row fails validation, log the error and continue with the next row.
   - Maintain a count of errors. If the count exceeds **25%** of the total rows, throw a `HitErrorsThresholdException`.
   - Execute the batch insertion using `executeBatch()`.
   - If `executeBatch()` throws an exception, keep the accounting there for making sure you are not hitting the threshold for insert errors - if you do then rollback the entire transaction. 
   - Display a summary of how many records were successfully inserted, how many failed due to errors, and the reason for failures.

6. **Bonus**:
   
   - Add logging to write error details to an "error_log.txt" file.  (this one will contain only the record that you failed to read successfully.) 
   - Do not worry about logging the records that you failed to insert. We only know the count for them - we don't / won't know the actual records that failed to insert successfully. x
   - Implement a retry mechanism to attempt inserting a failed row a specified number of times before giving up.

#### **Deliverables**:
- Java source code files implementing the above logic.
- SQL script for creating the `Trades` table.
- A sample trade data file (`trades_sample.csv`) with various types of valid and invalid rows for testing.
- An "error_log.txt" file that logs details of failed records.
- Write the Junit tests for this code as well.

#### **Expected Output**:
- The program successfully reads and inserts valid trade data into the database.
- If more than **25%** of the rows have errors, a `HitErrorsThresholdException` is thrown, and the batch insertion is rolled back.
- A summary is printed to the console indicating the number of records processed, number of successful inserts, and number of errors.

#### **Hints**:
- Use `BufferedReader` for reading the file.
- Use `String.split(",")` to parse each line.
- Use `try-catch` blocks to handle exceptions during parsing and insertion.
- Use JDBC `Connection` and `PreparedStatement` for database interactions.
- Implement batch processing using `addBatch()` and `executeBatch()` for efficiency.
- Use `setAutoCommit(false)` and `commit()` to manage transactions manually.

---

This assignment provides practice in file I/O, data validation, exception handling, and efficient database interaction using JDBC with prepared statements and batch processing.

---

### **Assignment Update: Dynamic Error Threshold Handling and Validation**

**Objective**: Extend the previous assignment to dynamically handle the error threshold. The program should be able to accept the error threshold from two different sources: command-line input and the application properties file. Validate the input in both cases, throwing the appropriate exceptions as specified.

### **Updated Requirements**:

#### **Case 1: Command-Line Input for Error Threshold**
1. **User Input**:
   - Accept the error threshold as a command-line argument.
   - Validate the input to ensure it is a `double` value between **1** and **100**.

2. **Exception Handling**:
   - If the input cannot be parsed as a `double` or falls outside the range of **1** to **100**, throw a **checked exception** called `InvalidThresholdValueException`.
   - When `InvalidThresholdValueException` is thrown, prompt the user for another input and retry until a valid threshold is provided.

#### **Case 2: Application Properties File for Error Threshold**
1. **Application Properties**:
   - Create an `application.properties` file in the classpath.
   - Define a property named `error.threshold` to specify the threshold value:
     ```
     error.threshold=25.0
     ```

2. **Reading and Validation**:
   - Read the value of `error.threshold` from the `application.properties` file using Java’s Properties class.
   - Validate the value to ensure it is a `double` between **1** and **100**.

3. **Exception Handling**:
   - If the value in the properties file is not a valid `double` or is outside the **1** to **100** range, throw a **runtime exception** named `InvalidThresholdRuntimeException`.
   - The program should terminate when `InvalidThresholdRuntimeException` is thrown, instructing the user to fix the `application.properties` file before re-running the program.

### **Implementation Details**:

1. **Threshold Input Handling**:
   - Use a command-line argument to pass the threshold (case 1).
   - Use `Properties` class to read `error.threshold` from `application.properties` (case 2).
   - Implement methods to validate and parse the threshold input, throwing the appropriate exceptions (`InvalidThresholdValueException` for case 1 and `InvalidThresholdValueRuntimeException` for case 2).

2. **Custom Exceptions**:
   - `InvalidThresholdValueException`: A **checked exception** for handling invalid command-line input. It should prompt the user to enter a new threshold value.
   - `InvalidThresholdValueRuntimeException`: A **runtime exception** for handling invalid values in the `application.properties` file. It should terminate the program execution and inform the user to correct the properties file.

### Deliverables**:
- Java source code implementing the main logic for handling both cases of threshold input.
- `application.properties` file with an example of a valid `error.threshold` value.
- Test cases to verify the correct handling of invalid command-line input and `application.properties` file content.

### **Expected Output**:
- For **Case 1**: If an invalid threshold is entered via command-line, the program will throw an `InvalidThresholdValueException`, prompt the user to enter a valid value, and continue until a correct threshold is provided.
- For **Case 2**: If an invalid threshold is found in `application.properties`, the program will throw an `InvalidThresholdValueRuntimeException` and terminate, informing the user to fix the `application.properties` file.
- Write the Junit tests for this code as well.

### **Hints**:
- Use `System.exit(1)` to terminate the program after throwing a runtime exception in case 2.
- Use `Properties` class to load properties from the classpath in Java.

This assignment covers reading configurations, exception handling, input validation, and the use of properties files, providing a comprehensive learning experience for handling different input sources in Java.



Here is an updated assignment to include a validation step against a securities lookup table during the database insertion process:

---

### **Assignment Update: Validating Securities Against Lookup Table**

**Objective**: Enhance the previous assignment to include a validation step during the database insertion. This step involves checking each security symbol against a lookup table (`SecuritiesReference`) to ensure the security is valid before inserting it into the `Trades` table.

### **Updated Requirements**:

1. **Securities Lookup Table**:
   - Create a database table named `SecuritiesReference` to store valid security symbols:
     ```sql
     CREATE TABLE SecuritiesReference (
         symbol VARCHAR(10) PRIMARY KEY,
         description VARCHAR(100)
     );
     ```
   - Populate this table with the list of valid securities symbols and descriptions.

2. **Security Validation During Insertion**:
   - For each trade record in the input file, before inserting it into the `Trades` table, check if the `ticker_symbol` exists in the `SecuritiesReference` table.
   - Use a `PreparedStatement` with a `SELECT` query to verify the presence of the security symbol in the `SecuritiesReference` table.
   - If the symbol is not found, log an error and skip the insertion for that particular record. This error will be counted towards the threshold error limit.

3. **Implementation Details**:
   - Modify the `processTradeFile(double threshold)` method to include a call to the database for each `ticker_symbol` to verify its validity.
   - If a `ticker_symbol` is not present in the `SecuritiesReference` table, log the error with a message like "Invalid security symbol: [symbol]" and continue processing the next record.
   - Maintain a count of errors. If the count exceeds the threshold (based on command-line input or properties file), throw the appropriate exception (`HitErrorsThresholdException` or `InvalidThresholdException`).

4. **Database Interactions**:
   - Use a `PreparedStatement` for querying the `SecuritiesReference` table:
     ```java
     String lookupQuery = "SELECT 1 FROM SecuritiesReference WHERE symbol = ?";
     ```
   - Use a `PreparedStatement` to batch insert valid trades into the `Trades` table.
   - Implement database transactions to handle batching and rollback if any error threshold is hit.


### **Expected Output**:
- The program successfully validates security symbols against the lookup table.
- Invalid symbols are logged as errors, and the error count is monitored against the specified threshold.
- If the threshold is exceeded, the appropriate exception (`HitErrorsThresholdException` or `InvalidThresholdException`) is thrown, and the database transaction is rolled back.

### **Hints**:
- Use JDBC `PreparedStatement` for querying and batch processing.
- Use `SELECT 1 FROM SecuritiesReference WHERE symbol = ?` to check for the presence of a security symbol.
- Utilize `conn.setAutoCommit(false)` for transaction management and rollback.

This updated assignment now incorporates database lookups for validation, enhancing the robustness and realism of the trade processing application.


Here is a sample CSV file content that you can use to import data into the `SecuritiesReference` table. This file contains some common securities symbols along with brief descriptions.

### **Sample CSV File: `securities_reference.csv`**

```csv
symbol,description
AAPL,Apple Inc.
GOOGL,Alphabet Inc.
AMZN,Amazon.com Inc.
MSFT,Microsoft Corporation
TSLA,Tesla Inc.
NFLX,Netflix Inc.
FB,Meta Platforms Inc.
NVDA,NVIDIA Corporation
JPM,JP Morgan Chase & Co.
VISA,Visa Inc.
MA,Mastercard Inc.
BAC,Bank of America Corp.
DIS,The Walt Disney Company
INTC,Intel Corporation
CSCO,Cisco Systems Inc.
ORCL,Oracle Corporation
WMT,Walmart Inc.
T,AT&T Inc.
VZ,Verizon Communications Inc.
ADBE,Adobe Inc.
CRM,Salesforce Inc.
PYPL,PayPal Holdings Inc.
PFE,Pfizer Inc.
XOM,Exxon Mobil Corporation
UNH,UnitedHealth Group Inc.
```

### **Instructions for Importing the CSV into the `SecuritiesReference` Table**
1. **Create the `SecuritiesReference` Table** (if not already created):
   ```sql
   CREATE TABLE SecuritiesReference (
       symbol VARCHAR(10) PRIMARY KEY,
       description VARCHAR(100)
   );
   ```

2. **Load the CSV Data into the Database**:
   - You can use MySQL's `LOAD DATA INFILE` command to import the CSV file:
     ```sql
     LOAD DATA INFILE '/path/to/securities_reference.csv'
     INTO TABLE SecuritiesReference
     FIELDS TERMINATED BY ','
     LINES TERMINATED BY '\n'
     IGNORE 1 ROWS
     (symbol, description);
     ```
   - Replace `'/path/to/securities_reference.csv'` with the actual path to your CSV file.

### **Note**:
- Ensure that the CSV file is accessible by the database server.
- Modify the column widths in the table creation script if you expect longer descriptions.



Here is the sample trade file with `trade_id` as an auto-incrementing integer:

### **Sample Trade File: `trades_sample.csv`**

```csv
trade_id,trade_identifier,ticker_symbol,quantity,price,trade_date
1,TDB_189234,AAPL,100,150.75,2024-09-01
2,TDB_134892,GOOGL,50,2800.55,2024-09-02
3,TDB_223456,AMZN,30,3450.20,2024-09-03
4,TDB_167893,MSFT,200,299.99,2024-09-04
5,TDB_198764,TSLA,10,720.15,2024-09-05
6,TDB_124567,NFLX,15,620.45,2024-09-06
7,TDB_209876,FB,25,365.90,2024-09-07
8,TDB_178945,NVDA,40,195.25,2024-09-08
9,TDB_150987,JPM,60,157.75,2024-09-09
10,TDB_230765,VISA,80,225.30,2024-09-10
```

### **Notes**:
- The `trade_id` column is now represented as a sequentially increasing integer starting from 1.
- This format assumes that the insertion into the database will handle the auto-increment behavior for the `trade_id`.