I was today years old when I knew about AppleScript. It appears it has been there since 1993. It is a proprietary scripting language developed by Apple that allows you to automate tasks and control applications on macOS. 

I am done dragging my vscode, terminal, browser and adjusting all to fit them in my dual screen. So the script gives me a workspace layout like below.

```bash
LEFT MONITOR                         RIGHT MONITOR

         75%       25%                        75%       25%
┌──────────────────┬───────┐       ┌──────────────────┬───────┐
│                  │       │       │                  │       │
│                  │       │       │                  │       │
│                  │       │       │                  │       │
│     FIREFOX      │ TERM  │       │     VS CODE      │CHATGPT│
│                  │       │       │                  │ EDGE  │
│                  │       │       │                  │       │
│                  │       │       │                  │       │
└──────────────────┴───────┘       └──────────────────┴───────┘

                          ~/Desktop/repo/Notes
```

```applescript
use framework "AppKit"
use scripting additions


-- ============================================================
-- CONFIGURATION
-- ============================================================

set projectFolder to POSIX path of (path to home folder) & "Desktop/repo/Notes"
set chatGPTURL to "https://chatgpt.com/"

-- Percentage of each monitor used by the large left-side window
set mainWidthPercent to 0.75


-- ============================================================
-- HELPER: WAIT UNTIL AN APP HAS A WINDOW
-- ============================================================

on waitForWindow(processName, maxAttempts)
	tell application "System Events"
		
		repeat with i from 1 to maxAttempts
			
			if exists process processName then
				
				tell process processName
					if exists window 1 then
						return true
					end if
				end tell
				
			end if
			
			delay 0.2
			
		end repeat
		
	end tell
	
	return false
end waitForWindow


-- ============================================================
-- HELPER: MOVE FRONT WINDOW
-- ============================================================

on moveFrontWindow(processName, xPos, yPos, windowWidth, windowHeight)
	
	if my waitForWindow(processName, 50) then
		
		tell application "System Events"
			tell process processName
				
				set frontmost to true
				
				set position of window 1 to {xPos, yPos}
				set size of window 1 to {windowWidth, windowHeight}
				
			end tell
		end tell
		
	end if
	
end moveFrontWindow


-- ============================================================
-- HELPER: MOVE VS CODE WINDOW CONTAINING PROJECT NAME
-- ============================================================

on moveVSCodeWindow(xPos, yPos, windowWidth, windowHeight)
	
	if my waitForWindow("Code", 50) then
		
		tell application "System Events"
			tell process "Code"
				
				set frontmost to true
				set foundNotesWindow to false
				
				-- Look specifically for a VS Code window
				-- containing "Notes" in the title
				
				repeat with currentWindow in windows
					
					try
						set windowTitle to name of currentWindow as text
						
						if windowTitle contains "Notes" then
							
							set position of currentWindow to {xPos, yPos}
							set size of currentWindow to {windowWidth, windowHeight}
							
							set foundNotesWindow to true
							exit repeat
							
						end if
						
					end try
					
				end repeat
				
				-- Fallback: use front VS Code window
				if foundNotesWindow is false then
					
					if exists window 1 then
						set position of window 1 to {xPos, yPos}
						set size of window 1 to {windowWidth, windowHeight}
					end if
					
				end if
				
			end tell
		end tell
		
	end if
	
end moveVSCodeWindow


-- ============================================================
-- DETECT SCREENS
-- ============================================================

set screenList to current application's NSScreen's screens()
set screenCount to (screenList's |count|()) as integer

if screenCount < 2 then
	
	display dialog "This workspace requires two monitors." buttons {"OK"} default button "OK"
	return
	
end if


-- ============================================================
-- FIND PHYSICAL LEFTMOST AND RIGHTMOST MONITORS
-- ============================================================

set leftScreen to missing value
set rightScreen to missing value

set lowestX to 9999999
set highestX to -9999999

set desktopTop to -9999999


repeat with screenIndex from 0 to (screenCount - 1)
	
	set currentScreen to screenList's objectAtIndex:screenIndex
	
	set visibleFrame to currentScreen's visibleFrame()
	set fullFrame to currentScreen's frame()
	
	set currentX to (current application's NSMinX(visibleFrame)) as integer
	set currentTop to (current application's NSMaxY(fullFrame)) as integer
	
	
	if currentX < lowestX then
		set lowestX to currentX
		set leftScreen to currentScreen
	end if
	
	
	if currentX > highestX then
		set highestX to currentX
		set rightScreen to currentScreen
	end if
	
	
	if currentTop > desktopTop then
		set desktopTop to currentTop
	end if
	
end repeat


-- ============================================================
-- LEFT MONITOR DIMENSIONS
-- ============================================================

set leftFrame to leftScreen's visibleFrame()

set leftX to (current application's NSMinX(leftFrame)) as integer
set leftMaxY to (current application's NSMaxY(leftFrame)) as integer

set leftY to desktopTop - leftMaxY

set leftWidth to (current application's NSWidth(leftFrame)) as integer
set leftHeight to (current application's NSHeight(leftFrame)) as integer


-- ============================================================
-- RIGHT MONITOR DIMENSIONS
-- ============================================================

set rightFrame to rightScreen's visibleFrame()

set rightX to (current application's NSMinX(rightFrame)) as integer
set rightMaxY to (current application's NSMaxY(rightFrame)) as integer

set rightY to desktopTop - rightMaxY

set rightWidth to (current application's NSWidth(rightFrame)) as integer
set rightHeight to (current application's NSHeight(rightFrame)) as integer


-- ============================================================
-- CALCULATE 75 / 25 SPLITS
-- ============================================================

-- LEFT MONITOR
set firefoxWidth to (leftWidth * mainWidthPercent) as integer
set terminalWidth to leftWidth - firefoxWidth


-- RIGHT MONITOR
set vscodeWidth to (rightWidth * mainWidthPercent) as integer
set edgeWidth to rightWidth - vscodeWidth


-- ============================================================
-- 1. OPEN VS CODE PROJECT
-- ============================================================

do shell script "open -a " & quoted form of "Visual Studio Code" & space & quoted form of projectFolder


-- ============================================================
-- 2. OPEN / ACTIVATE FIREFOX
-- ============================================================

tell application "Firefox"
	activate
end tell

delay 0.5


-- If Firefox is running but doesn't currently have a window,
-- create one with Command-N.

if my waitForWindow("Firefox", 10) is false then
	
	tell application "System Events"
		tell process "Firefox"
			set frontmost to true
			keystroke "n" using command down
		end tell
	end tell
	
end if


-- ============================================================
-- 3. RESET MICROSOFT EDGE
--
-- Close all existing Edge windows.
-- Then create exactly ONE ChatGPT window.
-- ============================================================

tell application "Microsoft Edge"
	
	activate
	
	delay 0.3
	
	set edgeWindowCount to count of windows
	
	if edgeWindowCount > 0 then
		
		repeat with i from edgeWindowCount to 1 by -1
			
			try
				close window i
			end try
			
		end repeat
		
	end if
	
	delay 0.5
	
	
	-- Create exactly one clean workspace window
	
	set chatWindow to make new window
	
	set URL of active tab of chatWindow to chatGPTURL
	
end tell


-- ============================================================
-- 4. RESET TERMINAL
--
-- Close all existing Terminal windows.
-- Then create exactly ONE Terminal in ~/Desktop/repo/Notes
-- ============================================================

tell application "Terminal"
	
	activate
	
	delay 0.3
	
	set terminalWindowCount to count of windows
	
	
	if terminalWindowCount > 0 then
		
		repeat with i from terminalWindowCount to 1 by -1
			
			try
				close window i
			end try
			
		end repeat
		
	end if
	
	
	delay 0.5
	
	
	-- Create one new Terminal window
	-- directly inside the project directory
	
	do script "cd " & quoted form of projectFolder
	
end tell


-- ============================================================
-- GIVE APPLICATIONS TIME TO FINISH OPENING
-- ============================================================

delay 2


-- ============================================================
-- 5. FIREFOX
--
-- LEFT MONITOR
-- LEFT 75%
-- ============================================================

my moveFrontWindow(¬
	"Firefox", ¬
	leftX, ¬
	leftY, ¬
	firefoxWidth, ¬
	leftHeight)


-- ============================================================
-- 6. TERMINAL
--
-- LEFT MONITOR
-- RIGHT 25%
-- ============================================================

my moveFrontWindow(¬
	"Terminal", ¬
	leftX + firefoxWidth, ¬
	leftY, ¬
	terminalWidth, ¬
	leftHeight)


-- ============================================================
-- 7. VS CODE
--
-- RIGHT MONITOR
-- LEFT 75%
-- ============================================================

my moveVSCodeWindow(¬
	rightX, ¬
	rightY, ¬
	vscodeWidth, ¬
	rightHeight)


-- ============================================================
-- 8. EDGE / CHATGPT
--
-- RIGHT MONITOR
-- RIGHT 25%
-- ============================================================

my moveFrontWindow(¬
	"Microsoft Edge", ¬
	rightX + vscodeWidth, ¬
	rightY, ¬
	edgeWidth, ¬
	rightHeight)


-- ============================================================
-- FINISH WITH VS CODE ACTIVE
-- ============================================================

tell application "Visual Studio Code"
	activate
end tell
```
