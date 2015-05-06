# history-api-fallback

## Introduction

Single Page Applications (SPA) typically only utilise one index file that is
accessible by web browsers: usually `index.html`. Navigation in the application
is then commonly handled using JavaScript with the help of the
[HTML5 History API](http://www.w3.org/html/wg/drafts/html/master/single-page.html#the-history-interface).
This results in issues when the user hits the refresh button or is directly
accessing a page other than the landing page, e.g. `/help` or `/help/online`
as the web server bypasses the index file to locate the file at this location.
As your application is a SPA, the web server will fail trying to retrieve the file and return a *404 - Not Found*
message to the user.

This tiny servlet filter addresses some of the issues. Specifically, it will change
the requested location to the index you specify (default being `index.html`)
whenever there is a request which fulfils the following criteria:

 1. The request is a GET request
 2. which accepts `text/html` and is not `application/json`
 3. is not a direct file request, i.e. the requested path does not contain a `.` (DOT) character
 
This project borrows heavily from the 
[connect-history-api-fallback](https://github.com/bripkens/connect-history-api-fallback) project.
