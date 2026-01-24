tinyGTC Toolkit V1.2 by Roger Need
=====================

A browser-based serial toolkit for the tinyGTC GNSS-disciplined counter/timer. It runs entirely in a modern Chromium-based browser and talks to the tinyGTC over USB serial using the Web Serial and File System Access APIs.

> Note: This program is released under the GNU GPLv3 (or later). You must keep the copyright and license header and release modifications under the same license.

***

## Features

- **Serial connection to tinyGTC**
    - Connects to any Web Serial–exposed COM port
    - Clean connect/disconnect logic with UI state reset.
    - Browser support check and warning if Web Serial is unavailable.
- **Live terminal with optional recording**
    - Scrollable terminal window showing text data from the tinyGTC.
    - Optional **“Record to File”** mode:
        - Streams terminal text to a user-chosen file in real time.
    - **“Save Log”** button:
        - Reads all terminal lines and writes out a text file.
    - **“Clear”** button to reset the visible terminal.
- **Monitor mode (continuous streaming)**
    - Starts/stops a background reader on the serial port.
    - Designed for continuous USB log or NMEA output from tinyGTC:
    - Optional **NMEA Decode** mode:
        - Parses common NMEA sentences: RMC, GGA, GSA, VTG, GSV, ZDA, TXT.
        - Produces human-readable summaries (fix status, lat/lon, speed, alt, mode, date/time).
        - Tracks satellites, HDOP, and fix quality.
- **GNSS SNR, Sky Plot and status display**
    - Dedicated SNR panel with:
        - Fix status (YES/No).
        - Satellites “in view” vs “used”.
        - HDOP value.
    - SNR bar chart:
        - Shows satellites grouped by constellation (GPS, BeiDou, GLONASS).
        - Color-coded bars and labels.
        - Only recently seen satellites are rendered (aging out after a timeout).
        - Highlights satellites actively used in the solution.
	- SkyPlot view
		- Shows satellite azimuth and elevation on polar chart
		- Filter buttons to show all sats, SNR >0, SNR>25 and NO SNR
- **Screen capture and PNG save**
    - **“Capture Screen”**:
        - Sends a `capture` command over serial to tinyGTC.
        - Shows a capture progress bar as data arrives.
		- Displays downloaded screen capture
   - **“Save PNG”**:
        - Prompts the user for a location and file name
        - Auto-generates a timestamped filename.
- **SD card file tools (on tinyGTC)**
    - **List SD Files**
        - Issues `sd_list` to the device.
        - Populates a clickable list in the terminal area.
        - Clicking a file name copies it into the filename input.
    - **Download File**
        - Issues `sd_read <filename>`.
        - Shows a download progress bar as raw bytes stream in.
        - Saves the file via File System Access API.
    - **Delete File**
        - Issues `sd_delete <filename>`.
        - Shows the device response in the terminal-style area.
- **Manual command entry**
    - Text box to send arbitrary commands to tinyGTC.
    - Splits the response into lines, appends them to the terminal.
- **UI/UX details**
    - Clean, centered layout with a “card” style main box.
    - Buttons are grouped logically:
        - Connection \& capture.
        - Monitor \& NMEA decode.
        - SD card tools \& terminal controls.
    - Lockout behavior:
        - Certain functions (capture, SD operations, send command) are disabled while monitor is running to avoid conflicting reads.
    - Terminal rendering:
        - Limits history to 200 lines
        - Auto-scrolls as new lines arrive.

## Browser Requirements

- A Chromium-based browser with:
    - Web Serial API enabled (Chrome, Edge, or compatible).
    - File System Access API support for save dialogs and streaming writes.
- HTTPS context or localhost (as required by these capabilities).
- On unsupported browsers, a warning banner is shown and functionality is disabled.

## Typical Workflow

1. **Open the HTML file** or use github URL in Chrome or Edge.
2. Click **“Connect to Device”** and select the COM port for the tinyGTC.
3. Use:
    - **Monitor** to see continuous USB log or NMEA output.
    - **NMEA Decode** to view human-readable GNSS status and SNR chart.
4. Use **Capture Screen** and **Save PNG** to grab and save the tinyGTC display.
5. Use **List SD Files**, **Download File**, and **Delete File** to manage SD card files on the device.
6. Use **Send Command** for manual SCPI/NMEA/diagnostic commands.
7. Optionally enable **Record to File** to log all terminal text as it arrives.
8. Use **Save Log** for a one-shot export of the current terminal contents.

***

## License

This program is free software: you can redistribute it and/or modify it under the terms of the 
**GNU General Public License** as published by the Free Software Foundation, either version 3 
of the License, or (at your option) any later version.

You must:

- Keep the copyright and license header.
- Release any modifications or derivative works under GPLv3 (or later).

See [https://www.gnu.org/licenses/gpl-3.0.html](https://www.gnu.org/licenses/gpl-3.0.html) for the full license text.

