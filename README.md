# Nostra SQLite

Standard SQLite with CMake support

This library is part of a project made by students of the htw saar (https://www.htwsaar.de/) and supervised 
by Dipl-Inf (FH) Christopher Olbertz.

GitHub: https://github.com/NostraTeam/SQLite

If you do not have the code yet, use the following command to clone the repository to your local
machine:  
```bash
git clone https://github.com/NostraTeam/SQLite.git
```` 
or download the ZIP-compressed directly from GitHub using the link above.

**This code uses an almost umodified version of the source code amalgamation that is provided by SQLite 
(www.sqlite.org). The NostraTeam is not the author of SQLite.**

The currently used SQLite version is 3.23.1.

## Changes from Standard-SQLite

This project uses the files "sqlite3.h" and "sqlite3.c" from the SQLITE code amalgamation. Both of these 
files have been modified to allow the exportation of symbols into a shared library file. **The files have not
been modified in any other way and any other files in this repository have been created by the NostraTeam.**