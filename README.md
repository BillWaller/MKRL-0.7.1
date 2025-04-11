# MKRL-0.7.1

Create Record Layouts from COBOL Data Structures

#### by Bill Waller

**MKRL** creates record layouts containing the position, format, and length of each named data item from COBOL data structures, such as File Descriptors.

- Developed and tested with **GNUCOBOL 3.3**.

- Requires **GNUCOBOL 3.2 or greater**.

- usage: **mkrl.sh** [-nr] File-Specification (full path and filename)

## Example:

Assume you want to create a record layout from a data structure. In this example, the first line of our data structure is a level 01 group name, **Sysdates-File-Record**.

>     01  Sysdates-File-Record.

* Save the data structure in a file, with an extension, **.DS**, in the **MKRL** directory. In this case, we will name our input file: **SYSDATES.DS**. Only lines beginning with leading spaces followed by a level-number will be processed. 

* Change to the MKRL directory and type:

>     ./mkrl.sh ../CPY/SYSDATES.DS

* View the record layout in **SYSDATES.RL**

>     view SYSDATES.RL

## How it works

:one:	In the **MKRL** directory, **mkrl.sh** copies the file containing the target data structure, **SYSDATES.DS** to **TMP.DS**.

:two:	**DS-PP** preprocesses **TMP.DS**, writing its output in **DS.DS**.

:three:	**DS-PARSER** parses **DS.DS**, transforming each data item into COBOL source code, which it writes to **DS-ANALYZER.CBL**.

:four:	**DS-ANALYZER.CBL** is incorporated via a copy directive into **RL.CBL** during compliation.

:five:	The output file name, **SYSDATES.RL** is derived by replacing the **.DS** extension of the input file name with **.RL**. The compiled COBOL program, **RL** uses the **GNUCobol runtime library** to analyze the data structure described by **DS-ANALYZER**, producing the record layout, which it writes to **SYSDATES.RL**. 

eMail [Bill Waller](billxwaller@gmail.com)
