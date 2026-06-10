# MPG-Cycle-Time-Study
Cycle Time Study Web App
A single-file browser-based web app for conducting cycle time studies, capturing manual or continuous-flow process timing, estimating downtime, projecting production impact, and reviewing bottlenecks through charts and process summaries.
This version is styled for Millennium Print Group with an MPG-inspired black theme, mobile-first capture improvements, and graph viewing support for mobile devices.
---
Purpose
The Cycle Time Study Web App is designed to help manufacturing, engineering, and operations teams collect process timing data directly from the floor.
It supports:
Manual start/stop process timing
Continuous-flow machine speed tracking
Known machine speed entry
Downtime estimation
Labor utilization review
Shift or daily production projection
Mobile capture workflow
Browser autosaves organized by study information
JSON export/import for sharing or backup
---
Main Features
Study Information
Each study includes a Study Information section used to identify and organize autosaves.
Fields include:
Study Title
Observer
Date
Shift
Location
Production Line
These fields are used to build clear browser autosave tags, such as:
```text
Study Title | Location | Production Line | Shift | Date | process count / capture count
```
This allows multiple studies to be saved in the same browser and reloaded later without relying on a single overwrite slot.
---
Browser Autosaves
The app stores studies locally in the browser.
Autosaves are created and updated as users work, including changes to:
Study information
Process setup
Timing captures
Projection settings
Continuous-flow settings
The app includes:
Browser Autosaves dropdown
Load Selected Study button
Delete Selected Save button
Current Autosave Tag display
> Note: Browser autosaves are stored in local browser storage. Clearing browser data may remove saved studies. Use Export Study JSON for backup.
---
Process Types
The app supports two main process types.
Start / Stop Process
Use this for manual or repeated-cycle work where each cycle has a clear start and stop.
Examples:
Manual assembly step
Packing process
Inspection station
Load/unload operation
Capture workflow:
Select or create a process.
Press Resume Capture.
Press Start Capture or Start Cycle.
Press Stop Cycle after each completed cycle.
Press Stop Capture or return to the dashboard.
Downtime is calculated as:
```text
Capture window time - completed cycle time
```
---
Continuous Flow Process
Use this for machinery or automated processes that run continuously and do not have a normal start/stop cycle for each unit.
Examples:
Slitter
Conveyor-fed machine
Automated robot cell
Continuous production equipment
Continuous processes can use either:
Timestamp marks
Known machine speed
Continuous processes display as vertical speed marker lines on the cycle time chart instead of regular process bars.
A continuous process can be changed back to Start / Stop later if the process needs to be reformatted.
---
Known Machine Speed
For continuous-flow equipment, users can enter a known machine speed instead of manually timestamping the process.
Example entries:
```text
1 unit every 2.5 seconds
60 units every 1 minute
3600 units every 1 hour
```
The app converts known speed into an estimated cycle interval and uses that value for throughput and charting.
---
Workers per Process
This field represents the direct labor assigned to the process during observation.
Recommended entries:
Situation	Entry
Manual station with one operator	1
Two-person manual process	2
Fully unattended machine	0
One operator covers four machines	0.25
One operator covers two machines	0.5
Worker count affects labor calculations such as:
Observed man-hours
Idle man-hours lost
Labor utilization
Idle labor cost
Worker count does not reduce machine throughput calculations.
---
Process Count per Production Line
This field represents parallel process capacity.
For manual work, it may mean multiple people or stations doing the same operation in parallel.
For continuous equipment, it may mean parallel machines or independent lanes.
Recommended entries:

Situation	Entry
One machine feeding the line	1
Two identical machines feeding the same flow	2
Four independent lanes, speed entered per lane	4
Four-lane machine, speed entered as total output	1
Use a value greater than 1 only when the entered speed is per machine, per lane, or per parallel process.
---
Metrics
The dashboard calculates:
Throughput Estimate
Average Man-Hour Utilization
Bottleneck Process
Total Captured Cycles / Marks
Total Observed Man-Hours
Idle Man-Hours Lost
Total Downtime
Idle Labor Cost Estimate
---
Projection Calculations
The app includes an Available Shift / Daily Time entry that projects study findings to a larger time window.
Users can enter available production time in:
Hours
Minutes
Projection logic:
```text
Projection Factor = Available Shift or Daily Time / Observed Capture Time
```
Projected downtime:
```text
Observed Downtime × Projection Factor
```
Projected idle man-hours:
```text
Observed Idle Man-Hours × Projection Factor
```
Projected idle labor cost:
```text
Projected Idle Man-Hours × Burdened Labor Rate
```
Projected production:
```text
Bottleneck Throughput × Available Time
```
---
Charts
The app includes two main charts.
Process Cycle Time Chart
Shows average cycle time by process.
Chart behavior:
Start/stop processes display as solid horizontal bars.
Slowest process is red.
Faster processes transition toward green.
Continuous-flow processes display as teal vertical speed marker lines.
Continuous-flow process names are shown near their marker lines.
Downtime per Cycle Chart
Shows average downtime per cycle by process.
For continuous known-speed processes, downtime may show as zero unless capture sessions record idle time.
---
Mobile Workflow
The app is designed to support mobile use on the production floor.
Mobile-friendly features include:
Compact MPG header
Large capture buttons
Mobile process cards
Resume Capture button on each process card
Graphs hidden from the main mobile dashboard by default
View Graphs button opens charts in a larger modal window
Horizontally scrollable graph view inside the modal
Recommended mobile flow:
Open or create a study.
Fill in Study Information.
Create a process.
Tap Resume Capture.
Use the large capture buttons to collect timing.
Return to the dashboard to review metrics.
Use View Graphs when chart review is needed.
---
Saving and Exporting
Browser Autosave
Autosaves happen automatically in the browser.
Use browser autosaves for quick recovery during field use.
Export Study JSON
Use Export Study JSON for backup or sharing.
The exported file contains:
Study information
Process definitions
Timing cycles
Capture sessions
Continuous marks
Projection settings
Import Study JSON
Use Import Study JSON to reload a previously exported study.
---
Deployment
This app is a single HTML file.
To use it locally:
Download the HTML file.
Open it in a modern browser.
Start a new study or import an existing JSON file.
To deploy through GitHub Pages:
Rename the app file to `index.html`.
Add it to a GitHub repository.
Enable GitHub Pages from the repository settings.
Open the generated GitHub Pages URL on desktop or mobile.
No server or database is required.
---
Browser Compatibility
Recommended browsers:
Chrome
Edge
Safari
Mobile Chrome
Mobile Safari
The app uses browser local storage for autosaves, so private browsing or strict browser storage settings may prevent autosaves from persisting.
---
Data Notes
This app is intended for observational study and estimation. Projection accuracy depends on:
Quality of timing samples
Whether the observed window is representative
Correct worker count entries
Correct process count entries
Correct known machine speed entries
Actual available production time
Real downtime patterns across the full shift or day
For stronger validation, compare projected results against actual production data after the study.
---
Suggested File Naming
Recommended naming pattern for exported JSON files:
```text
cycle-time-study-[location]-[line]-[date].json
```
Example:
```text
cycle-time-study-weck-slitter-24-2026-06-10.json
```
---
Version Notes
Current major updates include:
MPG black-theme styling
Mobile process cards
Mobile graph modal
Multi-study browser autosaves
Study Information tagging
Continuous-flow process support
Known machine speed support
Shift/daily projection calculations
Improved date picker visibility
Adjustable continuous-flow process type
Chart text overlap protection
