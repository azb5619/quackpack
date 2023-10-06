# Scripting

## Powershell
- Scope
    - Global: system wide
    - Script: file wide
    - Local: the current scope
    - Child scopes are visible from the parent scopes
    - Parent scopes are visible from child scopes unless made private
    - Items cannot be modified outside their scope
- Operators
    - ```-Not```
    - ```-eq```
        - equals
    - ```-le```
        - less than or equal to
    - ```-ge```
        - greater than or equal to
    - ```$True```
    - ```$False```
- Variables
    - Stores data
    - ```$[VAR] = [value]```
    - Parameters
        - ```Param($[VAR])```
        - ```
        Param(
            [Parameter(Mandatory, HelpMessage = "[message]")]
            [type]$[VAR]
        )
        ```
        - ```./[program name].ps1 -VAR '[value]'
    - Arrays
        - $[VAR] = [0], [1], [2], ...
        - ```$[VAR][0]``` returns ```[0]```
- Flow control
    - ```If```, ```ElseIf```, ```Else```
    - ```
    If ([condition] {
        [do stuff]
    } ElseIf ([condition]) {
        [do something else]
    } Else {
        [do another thing entirely]
    }
    ```
- Loops
    - For and Do-While
    - ```
    for([init]; [condition]; [repeat]) {
        [do something]
    }
    ```
    - ```do {[something]} while ([condition])```
    - ```do {[something]} until ([condition])```
- Error Handling
    - ```Try```, ```Catch```, ```Finally```
        - ```
        Try {
            [try]
        } Catch [System.IO.IOException] {
            [whoops]
        } Finally {
            [tidy up]
        }
        ```
    - ```Trap```
    - ```Throw "[message]"```
        - Throws an error
    - ```-ErrorAction [Action]```
- Functions
    - Named list of statements
    - ```
    function [ApprovedVerb]-[SingularNoun] {
        [do stuff]
    }
    ```
    - ```Get-Verb | Sort-Object -Property Verb```
        - Returns a list of approved verbs for function names
- Printing
    - ```Write-Host [data]```
    - ```Write-Error [data]```
    - To print a string use ```"[string]"```
    - To print a variable use ```"$[VAR]"```
    - To print an expression use ```"$([expression])"
    - To escape characters use ```"`[escaped character]"``` or ```'[literal string]'```
    - To print an error message use "$($_.exception.message)"
- Files
    - ```New-Item -Path [path] -Name "[name]" -ItemType "[file, directory, etc]"
        - Create a new file, directory, etc., at [path] with the filename [name]
    - ```Test-Path [path]```
        - Check to see if path [path] exists
    - Get-Content "[filename, function, etc.]"
        - Reads contents of file, function, etc.
    - ```Remove-Item [filename]```
        - Deletes a file

## Batch

Start a Batch script with ```@ECHO off``` for your sanity's sake.
Run a Batch script with ```./[script_name].bat``` or ```./[script_name].cmd```

- Batch Commands
    - ```DIR```
        - list all the files/directories in the current working directory
    - ```CD [directory]```
        - change directory; move to a different directory
    - ```EXIST "[filename]"```
        - Check that a file/folder exists
    - ```CLS```
        - clear terminal screen
    - ```ECHO [string]```
        - prints to terminal screen
    - ```@[COMMAND]```
        - hides which command is running
    - ```REM [comment]```
        - a comment

- Operators
    - ```EQU```
        - EQUals
    - ```NEQ```
        - Not EQual to
    - ```GEQ```
        - Greater than or EQual to
    - ```LEQ```
        - Less than or EQual to
    - ```&&```
        - And
    - ```||```
        - Or
    - ```NOT```
    - ```"%[var]%"=="[string]"```
        - String comparison
    - ```/I "%[var]%"=="[string]"```
        - Case insensitive string comparison

- Variables
    - Integers
    - Strings
    - ```SET [variable_name]=[value]```
    - ```SET /A [variable_name]=[expression]```
    - ```SET```
        - Lists all (static) variables for current command session
    - Read command line arguments with ```%[0-9]```
        - ```%0``` returns the filename

- System Varibles
    - ```PATH```
    - ```ERRORLEVEL```
    - ```DATE```
    - ```RANDOM```
    - ```TEMP```

- Flow Control
    - ```
    IF [CONDITION] (
        [do stuff]
    ) ELSE (
        [other stuff]
    )
    ```
    - ```EXIT [code]```
    - ```EXIT /B [code]```
        - Exits current batch script context rather than the command prompt process
    - ```GOTO :[label]```
        - ```:[label]``` sets a label to go to
    - ```GOTO :EOF```
        - Exits current batch script with return code ```1```
    - ```FOR %[VAR] IN ([ITERABLE]\*) DO [SOMETHING] %[VAR]
        - ```/D``` Directories
            - ```FOR /D %I IN (%USERPROFILE%\*) DO @ECHO %I
        - ```/R``` Recursive

- """Functions"""
    - ```
    CALL :func
    EXIT /B %ERRORLEVEL%

    :func
    ECHO "hello"
    EXIT /B 0
    ```

- Printing
    - ```ECHO [string]```
    - ```ECHO %[variable]%```

## Bash

It is good practice to start a Bash script with ```#! /bin/bash```
Run a Bash script with ```./[script_name].sh```

- Commands
    - ```echo [string, var]```
        - Print string, var
    - ```$([command])```
        - Run [command] in separate shell
    - ```cd [directory]```
        - Change directory
    - ```ls```
        - List all the files in the current directory
    - ```touch [filename]```
        - Create a new file
    - ```exec [program]```
        - Execute program
    - ```exit [code]```
        - Exit with code [code]
    - ```export [ENVVAR]=[value]```
        - Set an environment variable

- Variables
    - [var]=[value]
    - To access command-line arguments use ```$[0-9]```
        - ```$0``` returns the filename

- Flow Control
    - ```
    if [condition]; then
        [do stuff];
    elif [condition]; then
        [do something else];
    else [other stuff];
    fi
    ```
    - ```for [var] in [iterable]; do [commands]; done```
    - ```for (( [expr1] ; [expr2] ; [expr3] )) ; do [commands] ; done```
    - ```while [condition]; do [something]; done```
    - ```until [condition]; do [something]; done```
    - ```
    case [var] in
        [pattern]) [command];;
    esac
    ```
    - ```
    select [var] in [pattern];
    do
        [command];
        break;
    done
    ```
    - ```function [name] () {
            [commands]
        }
        ```
