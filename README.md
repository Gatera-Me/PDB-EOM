# PDB-EOM
Oracle Enterprise Manager (OEM) is a comprehensive management tool provided by Oracle for monitoring and managing Oracle databases, applications, and systems.A Pluggable Database (PDB) is a portable, self-contained database that resides within a Container Database (CDB) in Oracle's Multitenant architecture, introduced with Oracle Database 12c.


 SQL Commands and Explanations

 Selecting the Instance Name
```sql
select instance_name from v$instance;
```
- Purpose: This command retrieves the name of the current instance.
- Output: `orcl1` indicates the current database instance name.

 Show the Current Container Name
```sql
show con_name;
```
- Purpose: Displays the name of the current container.
- Output: `CDB$ROOT` indicates that you are connected to the root container of the CDB.

 Show All Pluggable Databases (PDBs)
```sql
show pdbs;
```
- Purpose: Lists all PDBs in the container database (CDB).
- Output: Lists `PDB$SEED`, which is in `READ ONLY` mode and indicates no other PDBs are open.

 Select PDB Name and Status from CDB View
```sql
select pdb_name, status from cdb_pdbs;
```
- Purpose: Retrieves the names and statuses of all PDBs in the CDB.
- Output: Only `PDB$SEED` is shown, which is `NORMAL`.

 Show Database Name and Open Mode
```sql
SELECT NAME, OPEN_MODE FROM V$DATABASE;
```
- Purpose: Displays the database name and its open mode.
- Output: Shows `ORCL1` in `READ WRITE` mode, meaning it's available for data manipulation.

 Retrieve Specific Database Parameters
```sql
SELECT NAME, VALUE FROM V$PARAMETER WHERE NAME IN ('db_create_file_dest', 'control_files', 'db_recovery_file_dest');
```
- Purpose: Retrieves essential database parameters like the locations for creating files and recovery.
- Output: Shows the control files and directories for the database files.

 Create New Pluggable Databases
```sql
CREATE PLUGGABLE DATABASE pdb1 ADMIN USER pdbadmin IDENTIFIED BY gatera;
CREATE PLUGGABLE DATABASE plsql_class2024db ADMIN USER pdbadmin IDENTIFIED BY gatera;
```
- Purpose: Creates two new PDBs named `pdb1` and `plsql_class2024db` with an admin user `pdbadmin` and password `gatera`.
- Output: Confirms that both PDBs were successfully created.

 Commit Changes
```sql
commit;
```
- Purpose: Finalizes any changes made (if applicable) to the database.
- Output: Confirms the commit was successful.

 Show Updated List of PDBs
```sql
show pdbs;
```
- Purpose: Displays the updated list of PDBs after creation.
- Output: Shows `PDB$SEED`, `PLSQL_CLASS2024DB`, and `PDB1` in `MOUNTED` mode.

 Open All Pluggable Databases
```sql
ALTER PLUGGABLE DATABASE ALL OPEN;
```
- Purpose: Opens all mounted PDBs.
- Output: Confirms that the operation was successful.

 Show Updated Status of PDBs
```sql
show pdbs;
```
- Purpose: Displays the current status of all PDBs.
- Output: All created PDBs are now in `READ WRITE` mode.

 Select the Name and Open Mode of All PDBs
```sql
SELECT name, open_mode FROM v$pdbs;
```
- Purpose: Retrieves the names and open modes of all PDBs.
- Output: Shows that both `PLSQL_CLASS2024DB` and `PDB1` are in `READ WRITE` mode.

 Set Current Session to a Specific PDB
```sql
ALTER SESSION SET CONTAINER = plsql_class2024db;
```
- Purpose: Changes the current session context to the specified PDB.
- Output: Confirms the session has been altered.

 Create a New User in the Current PDB
```sql
CREATE USER ir_plsqlauca IDENTIFIED BY gatera;
```
- Purpose: Creates a new user in the current PDB (`plsql_class2024db`).
- Output: Confirms the user was successfully created.

 Grant All Privileges to the Newly Created User
```sql
GRANT all privileges to ir_plsqlauca;
```
- Purpose: Grants all privileges to the newly created user, allowing full access to the database.
- Output: Confirms that the privileges were granted successfully.

 Drop the Pluggable Database
```sql
DROP PLUGGABLE DATABASE ir_to_delete_pdb INCLUDING DATAFILES;
```
- Purpose: Deletes the specified PDB (`ir_to_delete_pdb`) and removes its associated data files.
- Output: Confirms that the PDB was dropped successfully.

Conclusion
The sequence of commands executed demonstrates the creation, management, and deletion of Pluggable Databases in Oracle. Proper privileges were granted to users, and all operations were successfully completed. You now have a well-structured approach to managing PDBs, which will be beneficial for your ongoing database tasks. If you need any further assistance or explanations, feel free to ask!


