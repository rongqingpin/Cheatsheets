#### MS Access

Connecting to MySQL database:
1. [Download](https://dev.mysql.com/downloads/connector/odbc/) and install MySQL connector/ODBC
    - notice if office is 32-bit, install 32-bit ODBC even if system is 64-bit
2. Go to `Control Panel` - `Administrative Tools` - `ODBC Data Sources`
    - open the 32 / 64 version same with office, not windows
3. Add new source by configuring `TCP/IP Server` (url of MySQL server), `User`, `Password`, `Database`; use `Test` to confirm connection
    - [more details](https://kb.iu.edu/d/amsw)
4. Add `External Data` in MS Access: the source just added should show up in `ODBC Database` - `Machine Data Source`; if not, previous configuration wan't done correctly
