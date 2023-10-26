# Plex-Automatic-Preroll

All credits goes to **TheHumanRobot**

I WILL NOT MAINTAIN THIS REPOSITORY

## Docker version

There you go : https://hub.docker.com/r/thehumanrobot/rollarr/

## Dev branch
This branch should be stable but you have been warned!

This new branch contains an almost fully rewritten code base. This now allows for Pre-rolls by Month, Week, Day, Misc, and Master list. The config is now based on yaml instead of a ini file for easier reading and data config data storage.

Thanks to [@agrider]( https://github.com/agrider ) for masterlist re-ordering and empty path error handling

## Requirements
-[Python 3.7+](https://www.python.org/)
(Probably works on a lower version haven't tested)

-[PlexAPI](https://github.com/pkkid/python-plexapi)


## Installation
First make sure you have Python installed version 3.7 and above. Next run:


```
pip3 install -r requirements.txt
```
That will install all the needed packages 

## Step by step instructions by Danny at smarthomepursuits.com

https://smarthomepursuits.com/configure-plex-automatic-prerolls-on-windows/

## Settings
The config.yml file is created through the script for ease of use. Optionaly you can just create it by hand by filling in the exampleconfig.yml file and then renaming it to config.yml. If you need to update it than you can edit the config.yml file.

Below is an example of the config file:
```
Plex: 
  url: https://url:32400
  token: 
MasterList: 
  UseMaster: No
  MasterRandom: No
  # If the path for the Master List is left blank the script will create the path 
  # based on if Monthly, Weekly, or Daily are set to be used in the Master List 
  # otherwise you can populate the path with your own set of trailers and if month, week, day or misc is left blank it will call the master list
  Path: 
Monthly: 
  Jan: /path/to/file.mp4
  Feb: 
  Mar: 
  Apr: 
  May: 
  June: 
  July: 
  Aug: 
  Sept: 
  Oct: 
  Nov: 
  Dec: 
  MasterList: No
  MasterListValue: 
  UseMonthly: Yes
Weekly:
  StartDate: 
  EndDate: 
  Path: 
  MasterList: No
  UseWeekly: No
Daily:
  StartDate: 
  EndDate: 
  Path: 
  MasterList: No
  UseDaily: No
Misc:
  Path: 
  StaticTrailer: /trailer/to/play/at/end.mp4
  #Enter the number of trailers to use ex: Path contains 5 trailers you set this value to 2 the program will pick two at random as well as the static trailer to play in order:
  TrailerListLength: 
  UseMisc: No
```

**If you want multiple random pre-roll videos to play in a specific month, week, or day all you need to do is seperate the paths with a semi-colon for the master list you need to specify random or not if allowing the script to make it automatically**
Example when it ask you to add the December trailer path and you want to play two videos randomly for that month type:

```
/path/to/file1.mp4;/path/to/file2.mp4
```
**Example config will be provided**

**The order of which it chooses the trailer list goes Misc, Daily, Weekly, Monthly, and then Master **

For example you could have your monthly list set up to play a specific set of pre-rolls for 3 months of the year leave the rest blank and those empty months will use the masterlist. While also set it using the Daily section to play a specific pre-roll on Dec 25th and then even have it so for 2 weeks during Dec it rotates through a set of pre-rolls defined in the Weekly pre-roll section.

## Usage

### Setting Plex Preroll

You need to schedule a job for updating the preroll each day, week, or month depending how you want your pre-rolls updated.

**macOS or Linux:**
Ex: Monthly

```
crontab -e
0 0 * 1-12 * python3 /path/to/scripts/Plex_Trailers.py 2>&1
```

**Windows:**

Verify python is added to the PATH environmental variable
Search for task schedular and open it. Click "Create Basic Task" and enter a name and description. Then set the task to run monthly. Choose "Start a program" then for "Program/script" add the full path of the Plex_Trailers.py script Click "Finish" and you are done!


## Running For The First Time

Since you just downloaded the script the first time you run it you will be prompted to fill in some information to create the config file unless you fill out the exampleconfig.yml file and then rename it to config.yml.

```
python3 /path/to/scripts/Plex_Trailers.py
```

I hope this is useful for some people and feel free to modify it for your own use!
