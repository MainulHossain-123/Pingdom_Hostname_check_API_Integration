# Pingdom_Hostname_check_API_Integration
Plug and Go Python Script for running multiple sites Pingdom Checks concurrently and generating the output to a CSV file

## Note
The code, is for downloading Pingdom Checks returned by the Single check API but this can be modified to enter more parameters and to even run daily checks on all possible pingdom checks under an organization on a daily basis.

## Prerequisites 
* **Python 3.12 or higher**. Download it from https://www.python.org/downloads/
* **IDE** - I personally used Visual Studio Code but it is upto your preference.
* **Libraries - aiofiles**: Run in Terminal of enviornment or in command prompt **pip install aiofiles**
* **Libraries - aiohttp**: Run in Terminal of enviornment or in command prompt **pip install aiohttp**
* **Libraries - asyncio**: Run in Terminal of enviornment or in command prompt **pip install asyncio**
* **Libraries - csv**: Run in Terminal of enviornment or in command prompt **pip install csv**
* **Pingdom API Key**. You must have the API key enabled with minimum Read permissions from your Pingdom account.

## Languages, Frameworks and API calls used in the script
The Script uses the following:

- *[Python 3.12.3](https://www.python.org/downloads/release/python-3123/)* as the primary Programming Language.
- *[Visual Studio Code](https://code.visualstudio.com/download)* as the IDE.
- *[Pingdom Version 3.1 API Single Check](https://docs.pingdom.com/api/?_ga=2.230003480.509660209.1590495493-1793431897.1589990976#tag/Single)* as the primary endpoint for primary Authorization header.
- *[Aiofiles Module](https://pypi.org/project/aiofiles/)* is an Apache2 licensed library, for handling local disk files in asyncio applications.
- *[Asyncio Module](https://docs.python.org/3/library/asyncio.html)* is used to make concurrent asynchronous calls to allow for high-performance network tasks to be completed for both client and web server applications, database connection libraries, distributed task queues, etc.
- *[Aiohttp Module](https://docs.aiohttp.org/en/stable/index.html)* is a sub framework, part of asyncio that works in tandem with asyncio for making concurrent multiple HTTP calls
- *[CSV Module](https://docs.python.org/3/library/csv.html)* allows us to write or read CSV files, in this case write all retrieved data to a CSV file.

## Legal
* This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Pingdom or any of its affiliates or subsidiaries. This is an independent and unofficial software. Use at your own risk. Commercial use of this code/repo is strictly prohibited.

## Basic Usage

### API_Key Replacement
Simply replace the value in **api_key** with your own API key and run the script. 

#Set your Pingdom API key
```
api_key = 'YOUR_API_KEY'
```

### User Input
The hostnames are entered via a user input with single or multiple hostnames being pinged at the same time. In case of multiple hostnames simply enter each hostname one by one with each seperated by a comma.
```python
target_urls_input = input("Enter the target URLs separated by commas: ")
target_urls = [url.strip() for url in target_urls_input.split(",")]
```

### Extracted data and CSV File
The data will be saved in a CSV file **pingdom_results.csv**, which you can change to your desire and also include a path for saving if you wish but by default. For the current code I am downloaind the following data target_url, status, probedesc, statusdesc, statusdesclong from the API JSON response, but if you wish you can customise the data according to your needs.
```python
if result_data:
                    status = result_data.get('status', 'N/A')
                    # probeid = result_data.get('probeid', 'N/A')
                    probedesc = result_data.get('probedesc', 'N/A')
                    statusdesc = result_data.get('statusdesc', 'N/A')
                    statusdesclong = result_data.get('statusdesclong', 'N/A')
                    await csv_writer.writerow([target_url, status, probedesc, statusdesc, statusdesclong])
```
