# MAGNETO

## Description

Incident response and forensic tool
Thank you for your interest. Please contact author for other essential files required to run this tool.

## Features

1. Parse and process triage output files, saving them in pgsql 
2. Process memory captures using volatility 
3. Parse and process volatility output files, saving them in pgsql 
4. Perform baseline, long tail analysis and correlation using above data, stored in pgsql

## Work-In-Progress

1. Identify CVE vulnerabilities based on software applications installed 
2. Upload file hashes to VT and automatically process unknown files through cuckoo 
3. Spoofed email identifier 
4. Windows Log Parser 
5. Windows malicious document identifier

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. 

### Step by Step Guide to power up MAGNETO on Windows

1. Download Magneto Files from "https://github.com/padfoot999/magneto"
2. Install Python 2.7 (32 bit)
3. Configure Python Path in Windows System Environment Variables
4. Install PostgreSQL
5. Go to PGAdmin, create server with the following setting
        <br />Name: "magneto"
        <br />Host name/Add: "127.0.0.1"
        <br />User name: postgres
        <br />Password: kpmg@123
6. Create "magneto" database within server
7. Install all necessary python modules (i.e. Pandas, psycopg2) using pip
8. Make sure that workstation has Powershell v4.0 and above installed

### SOP for Triage Post-Processing

1. Launch Ubuntu VM and process Memory (.raw) file using PROCESS_memory.py file. Dump Volatility output into the Evidence folder within each Incident folder.
2. Process Event Logs using Windows Powershell (WINTEL.ps1) file.
3. Run PROCESS_postTriage File (Outputs RegRipper, SRUM-DUMP, WebCache Files, MFT, JLECMD TSV File)
4. Run submit.py file
5. Run Baseline, ProcessDiff, ProcessNetworkConnections, AutoRunMerged, CVE Checker Python scripts
6. Run Summary file

## Running Magneto Scripts

### Python Magneto
* Post Triage
```
python PROCESS_postTriage.py -d <Path to Incident folder> -p <Project Name (i.e. RADIUM)>
```
* Submitting Incident Folders into Postgresql database
```
python submit.py -d <Path to Incident folder> -p <Project Name (i.e. RADIUM)>
```
* Output Baseline
```
python OUTPUT_baselineCSV.py -p <Project Name (i.e. RADIUM)>
python OUTPUT_baselineXLSX.py -p <Project Name (i.e. RADIUM)>
```
* Output Process Difference
```
python OUTPUT_processDifference.py -p <Project Name (i.e. RADIUM)>  
```
* Output Process Network Connections
```
python OUTPUT_processNetworkConn.py -p <Project Name (i.e. RADIUM)>  
```
* Output Process Network Connections
```
python OUTPUT_processNetworkConn.py -p <Project Name (i.e. RADIUM)>  
```
* Output Merged AutoRun Paths
```
python OUTPUT_autorunMerge.py -d <Path to Incident folder> -p <Project Name (i.e. RADIUM)>  
```
* Output cveChecker
```
python OUTPUT_cveChecker.py -p <Project Name (i.e. RADIUM)> 
python OUTPUT_cveChecker.py -p <Project Name (i.e. RADIUM)> -t <Image Name (i.e. 20170117115236 - AERO Incident)
```
* Output Summary File
```
python OUTPUT_summary.py -d <Path to Incident folder> -r <Output folder after running PROCESS_postTriage.py> -p <Project Name (i.e. RADIUM)>
python OUTPUT_summary.py -d "E:\\" -r "F:\\magneto v2\\results\\ARGON" -p ARGON
```
### WINTEL Powershell 
```
cd <Magneto WINTEL folder>
.\WINTEL_WindowsLogParser-v?.ps1 -logPath <...\Evidence\Logs)> -project <ARGON>
```
