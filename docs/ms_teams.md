Map the letter "H:" to your OneDrive:<br />
Create a script named "MapH.cmd" with the following content and place in the Startup Folder
  <span style="color: #3366ff;"></span><br />
  <span style="color: #3366ff;">@echo off</span><br />
  <span style="color: #3366ff;">REM ----------------------------------------------------------------------------</span><br />
  <span style="color: #3366ff;">REM Author: Robert Holland</span><br />
  <span style="color: #3366ff;">REM Name: MapH.cmd</span><br />
  <span style="color: #3366ff;">REM Creation Date: Thu Oct 14 2021 08:53:25 GMT-0700 (US Mountain Standard Time)</span><br />
  <span style="color: #3366ff;">REM Last Modified:</span><br />
  <span style="color: #3366ff;">REM Purpose: Locally Map H: drive to OneDrive</span><br />
  <span style="color: #3366ff;">REM ----------------------------------------------------------------------------</span><br />
  <br />
  <span style="color: #FF66AA;">Change the "OneDrive - Location" part to your specific settings.</span><br />
  <span style="color: #3366ff;">subst H: "C:\Users\%username%\OneDrive - Location\"</span><br />
