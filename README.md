# Coding a File Integrity Monitor | PowerShell

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53726783117/in/dateposted/" title="FIM"><img src="https://live.staticflickr.com/65535/53726783117_b0c65302c7_c.jpg" width="800" height="732" alt="FIM"/></a>

## Introduction
Ensuring the integrity of data stands as a foundational pillar of the CIA Triad for IT security systems. With this principle in mind, I embarked on a project to develop a File Integrity Monitor (FIM), aimed at reinforcing data integrity across organisational systems.

At the core of this initiative lies the implementation of file hashing—a technique akin to creating digital fingerprints for each file. These hashes serve as immutable identifiers stored within a baseline.txt file, forming a reliable reference point for data integrity verification.

Critical to the FIM's functionality is its ability to detect even the slightest alterations within files. When changes occur, the corresponding hash undergoes modification, triggering the FIM to promptly alert stakeholders. This proactive approach ensures that data integrity remains uncompromised, bolstering the overall security posture of the organisation.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53728033559/in/photostream/" title="FIM Flow Chart"><img src="https://live.staticflickr.com/65535/53728033559_100e3ac165_c.jpg" width="762" height="800" alt="FIM Flow Chart"/></a>

## Create script in PowerShell 
- Open PowerShell app and Run ISE as Administrator 
- To remove any current restricted policy type the command: Set-ExecutionPolicy RemoteSigned → press enter key
- Note: This will enable you to run PowerShell scripts from untrusted sources on your system
- Note: -eq means equals to
- Note Write-Host “” is to create a new line break
- Save your script as “Fim.ps1” and save it to the Desktop on your PC. 
- Open File Explorer and create a folder within the Desktop called “FIM”. Move Fim.ps1 into the FIM folder
- Note: The aim is to collect all files in the directory (FIM) we want to monitor

## Start Coding in Script Pane
- Click the Show Script Pane Top icon 
- Type the first block of code as seen in the image below or
- Copy & paste from this file Fim.ps1: https://github.com/LawEsan/PowerShell-FIM/blob/main/Fim.ps1
- Note: Remember to constantly test code by clicking the “Run Script” icon on the menu pane to ensure script is working free of any errors

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53726731822/in/dateposted/" title="1st code block"><img src="https://live.staticflickr.com/65535/53726731822_80683edf47_c.jpg" width="800" height="410" alt="1st code block"/></a>

## Create a new function that calculates the Hash file
- Create function Calculate-File-Hash
- Go to https://github.com/LawEsan/PowerShell-FIM/tree/main/Files → Save files on your PC
- Copy the path link to the a.txt file
- Change directory in PowerShell to the file location e.g run the “cd Desktop” command to change directory to Desktop. Run “ls” command to list files and alternate using both commands until you reach your file location.
- Run only the function code block. To do this, highlight the function code only and click the Run Selection icon.
- The a.txt file Hash will print to screen

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727981374/in/datetaken/" title="new function"><img src="https://live.staticflickr.com/65535/53727981374_bb6e06e9b0_c.jpg" width="800" height="413" alt="new function"/></a>

## Store Hash in a Variable
- Instead of printing the hash to screen, store it in a variable by following these steps:
- On the Script Pane type: $hash = Calculate-File-Hash “insert path to file here” → press enter key
- The Hash will be stored in the variable “$hash”
- In PowerShell console type: $hash → press enter key
- The Hash will print to screen
- You can now delete the line of code $hash = Calculate-File-Hash “insert path to file here”

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727638096/in/datetaken/" title="Calculate File Hash1"><img src="https://live.staticflickr.com/65535/53727638096_3755c33f74_c.jpg" width="800" height="411" alt="Calculate File Hash1"/></a>

## Gather all the files in the directory to monitor them
- You are going to gather all the hashes of the four .txt files  and store them in a single .txt file that has the path and file hash with it.
- Delete this line of code: Write-Host “Calculate Hashes, make a new baseline.txt” -Foreground Color Cyan
- Change directory in PowerShell console to FIM folder that holds the Files. To go one level back in your path use the command “Pop-Location” and type the exact path you wish to return too e.g Pop-Location C:\Users\lesan\Desktop\FIM
- In the Script Pane create a $files variable. 
- When you type “./“ at the end of the $files variable, the Files option will now appear
- Run the $files variable only → This will gather all four .txt files and print screen to console
- Delete $files 

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53726731662/in/datetaken/" title="Gather all files"><img src="https://live.staticflickr.com/65535/53726731662_0918c32e3b_c.jpg" width="800" height="410" alt="Gather all files"/></a>

## Get the Hashes of all files
- Use the $files variable in a foreach loop
- Create the loop with the code in this image
- Create a $f variable which will represent each .txt file. 
- Type foreach ($f in $files) { → make a new line  
- Type Calculate-File-Hash $f.FullName 
- Make “Calculate-File-Hash $f.FullName” a variable by typing “$hash =“ before it
- Run the code like the image below so that the file path and hash are displayed 

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727638051/in/datetaken/" title="file path + hash"><img src="https://live.staticflickr.com/65535/53727638051_fc6d7ffe5c_c.jpg" width="800" height="413" alt="file path + hash"/></a>

## Create baseline.txt file with all file paths and hashes inside

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53726731752/in/datetaken/" title="create baseline.txt"><img src="https://live.staticflickr.com/65535/53726731752_1dedc51c23_c.jpg" width="800" height="411" alt="create baseline.txt"/></a>

## Error handling 
- The problem now is that every time the script is run, the baseline will continue to unnecessarily add the same files that already exist in the folder.
- To prevent this, create a new Function in the beginning of the script that will delete the baseline.txt if it already exists.
- Run the script to test it works OK

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727638061/in/datetaken/" title="Error handling"><img src="https://live.staticflickr.com/65535/53727638061_1cfd1d2ebc_c.jpg" width="800" height="410" alt="Error handling"/></a>

## Begin monitoring files with saved Basedline.txt
- Load the file hash pairs from baseline.txt and store them in a dictionary
- Note: The dictionary is going to hold the file path and corresponding hash 
- Create the dictionary by typing code as seen in the image below

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53728081230/in/datetaken/" title="Create dictionary"><img src="https://live.staticflickr.com/65535/53728081230_d46085be75_c.jpg" width="800" height="412" alt="Create dictionary"/></a>

## Create variable $filePathsAndHashes to store content
- All the content (file path + hash) from the baseline.txt file must be stored in a variable $filePathsAndHashes
- As there are multiple files, create a variable called $f in a foreach loop.
- Run the script to test the $filePathsAndHashes variable is working

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727848628/in/datetaken/" title="Paths and Hashes"><img src="https://live.staticflickr.com/65535/53727848628_fbcb3b2ee5_c.jpg" width="800" height="412" alt="Paths and Hashes"/></a>

## Create an array to store each file 
- The “0” element of the array is the file path and the “1” is the hash
- When the script is run with the element “0” all file paths will t will be printed to screen. When the “0” is changed to a “1”
  
<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53726731787/in/datetaken/" title="Create array"><img src="https://live.staticflickr.com/65535/53726731787_fb50d12eb3_c.jpg" width="800" height="412" alt="Create array"/></a>


<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53726731777/in/datetaken/" title="Create array2"><img src="https://live.staticflickr.com/65535/53726731777_c782e878c2_c.jpg" width="800" height="412" alt="Create array2"/></a>

## Create infinite while loop 
- The while loop will check if any file has been modified
- Add a delay of one second so that the loop does not run too fast

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727981379/in/datetaken/" title="Infinite loop"><img src="https://live.staticflickr.com/65535/53727981379_cdc008314b_c.jpg" width="800" height="411" alt="Infinite loop"/></a>

## Calculate file hash and check within dictionary if the hash exists
- This code in the image below will get all files and put them in the $files variable. For each file the file hash will be calculated and that hash will be compared to what is in the dictionary (baseline.txt).
- If the hash is the same, that means the file remains unchanged and is still in its original form.
- If the hash is different, that means the file has been modified.
- If the hash does not exist that means the file has been deleted
- Run the script and enter ‘B’ when asked for user input
- Open File Explorer and navigate to the Files folder
- Create a new file called “e.txt” to test if script is working as a message that a new file has been created should appear in the console
- Delete “e.txt” and this should stopped the console from looping

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727848638/in/datetaken/" title="New file created e.txt"><img src="https://live.staticflickr.com/65535/53727848638_8f940183dc_c.jpg" width="800" height="412" alt="New file created e.txt"/></a>

## Notify if a new file has been changed
- Add the if and else conditions to your script as seen in the image below. 
- and enter ‘B’ when asked for user input
- Open File Explorer and navigate to the Files folder
- Open any file e.g “d.txt” and modify it by adding extra text then saving the file (Ctrl+S). This should trigger the alert we created “d.txt has changed!!!”
- Delete the extra text you added then save the d.txt file. This should stop the console from looping.
- Click Stop Operation icon (the red square)

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727638056/in/datetaken/" title="File has changed"><img src="https://live.staticflickr.com/65535/53727638056_ef167e75cb_c.jpg" width="800" height="412" alt="File has changed"/></a>

## Move the if and else conditions code block 
- Cut the if and else conditions code block
- Create an else statement and paste the code block so that it is within it 
- Change the # File has been compromised -ForegroundColor to Yellow
- Run the script and enter ‘B’ when asked for user input
- Open File Explorer and navigate to the Files folder
- Create a new file called “e.txt” → Verify the “file has been created” alert appears in the console
- Delete file “e.txt” → Console should stop looping
- Modify “d.txt” file and Save → Verify the “file has been changed” alert appears in the console
- Revert the “d.txt” file to its original state (delete the extra text you added) and Save → Console should stop looping

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727981389/in/datetaken/" title="Move if and else"><img src="https://live.staticflickr.com/65535/53727981389_194aeeeae9_c.jpg" width="800" height="415" alt="Move if and else"/></a>

## Create function to notify if a file has been deleted
- Create a foreach variable which will list all the file paths in the dictionary

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727637996/in/datetaken/" title="Foreach key"><img src="https://live.staticflickr.com/65535/53727637996_841fd486e4_c.jpg" width="800" height="410" alt="Foreach key"/></a>

- The file path we are checking still exists ($baselineFileStillExists) must be set to the variable $key. This is to verify if a file still exists in the dictionary
- Create an if NOT condition meaning if the file does NOT exist, notify the user

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53726731742/in/datetaken/" title="File deleted"><img src="https://live.staticflickr.com/65535/53726731742_e6e7877f63_c.jpg" width="800" height="410" alt="File deleted"/></a>

- Cut the code block “One of the baseline files must have been deleted” and paste it in another area so that it is outside the foreach loop
- Open File Explorer and navigate to the Files folder
- Open another File Explorer pane and navigate to any other directory e.g Music and keep both File Explorers open whilst you are running the script. 
- Run the script
- Move “d.txt” from its location to the Music directory. 
- An alert should appear on the console that the file d.txt has been deleted!
- Move the file back to it’s original location → Console should stop looping
- Modify “d.txt” file and Save → Verify the “file has been changed” alert appears in the console
- Revert the “d.txt” file to its original state (delete the extra text you added) and Save → Console should stop looping
- Create a new file called “e.txt” → Verify the “file has been created” alert appears in the console
- Move “e.txt” out to the Music file directory → Console should stop looping

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53727638036/in/datetaken/" title="Final"><img src="https://live.staticflickr.com/65535/53727638036_d22503f2b1_c.jpg" width="800" height="412" alt="Final"/></a>

## Conclusion
Using PowerShell, I've created an effective File Integrity Monitor (FIM) for this project. It ensures file data remains unchanged or undeleted. If any alterations occur, the FIM promptly raises specific alerts. This proactive approach enhances an IT system's security, addressing evolving threats and maintaining stakeholder trust.
