# ezg-deploy-software
Automated deployment

WORK FLOW:
DONE-Prompt if this is for CNR?
	DONE-No > Set log directory to generic location.
	DONE-Yes > Prompt for SNOW#?
		Verify if SNOW# directory exists, otherwise create it.
		DONE-Set log directory to SNOW# directory.
For each entry that matches the filter, perform the following:
	DONE-Output the Product Name & Latest Version & Path\Latest\Executable+Latest.exe
	DONE-Check to see if the Path\Latest\Executable+Latest.exe exists:
		DONE-0 (does not exist) > Alert the user that the software version cannot be found, and CONTINUE.
		DONE-1 (does exist) > Check to see if Product Name (regardless of version) is installed already:
			DONE-0 (not installed) > Check to see if the folder has an _Install.iss response file:
				DONE-0 (no _Install.iss file) > Execute latest (interactive), creating an _Install.iss response file.
				DONE-1 (_Install.iss file) > Execute latest, using the _Install.iss response file, creating a log file.
			DONE-1 (installed) > Check to see if Product is already on the latest:
				DONE-0 (not on latest) > Check to see if the folder has an _Update.iss response file:
					DONE-0 (no _Update.iss file) > Execute latest (interactive), creating an _Update.iss response file.
					DONE-1 (_Update.iss file) > Execute latest, using the _Update.iss response file, creating a log file.
				DONE-1 (on latest) > Notify the user that the software is up-to-date, and CONTINUE.

FUTURE ENHANCEMENTS
-Update the Get-ExcelData function to check for 32-bit or 64-bit provider to determine if "RunAs32" is necessary or not
-Modify summary to only display red if there's something bad (0 bad should not be in red; that's good!)
-Confirm WWW Service is stopped before proceeding...
-Verify the server is a FACAPP server; Use get-facetsservers function. Wouldn't want to accidentally update another type of server (FIC).
-Append Username to log file to determine who executed it.
-Compare spreadsheet "Latest" w/ actual latest in COTS Folder. Output to User, but continue. This is a safety precaution against an out-dated spreadsheet.
-Before launching ANY INTERACTIVE, verify if the current server is PROD; Use get-facetsservers function:
	-If PROD, we need to halt things because we should never be introducing new software directly into PROD w/o following the SDLC.
		-Unless, of course, it's a brand new PROD server build, not yet in production.
