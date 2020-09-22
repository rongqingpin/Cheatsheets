#### MS Access

Connecting to MySQL database:
1. [Download](https://dev.mysql.com/downloads/connector/odbc/) and install MySQL connector/ODBC
    - notice if office is 32-bit, install 32-bit ODBC even if system is 64-bit
2. Go to `Control Panel` - `Administrative Tools` - `ODBC Data Sources`
    - open the 32 / 64 version same with office, not windows
3. Add new source by configuring `TCP/IP Server` (url of MySQL server), `User`, `Password`, `Database`; use `Test` to confirm connection
    - [more details](https://kb.iu.edu/d/amsw)
4. Add `External Data` in MS Access: the source just added should show up in `ODBC Database` - `Machine Data Source`; if not, previous configuration wan't done correctly

Connecting to Access with Python:
1. follow steps 1 & 2 from above to set up Access database drive 
2. if 32-bit access drive is installed, must use 32-bit python
    - install 32-bit python without adding it to system path
    - go to python path to install pip (installed under `python32_path\Scripts\`)
    - `Scripts\pip` to install virtualenv
    - `Scripts\virtualenv \path\to\env -p path\to\python_32Version.exe`
    - switch to new virtual environment 
3. follow python sql commands in `sql.md`
