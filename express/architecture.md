# Architecture
This guide details how files and folders are structured and named.

## Folder structure
Here is an example of a good folder structure.
- ./
  - **controllers/**
     - _index.js_  
     - test.js
     - route1.js  
     - route2.js  
     - route3/  
       - _index.js_
       - _route3_test.js_
       - route4.js
       - route5.js
  - **middleware/**
    - auth/
      - _index.js_
      - user.js
      - admin.js
      - passport.js
    - session.js
    - error.js
  - **helpers/**  
    - promise-handler.js
    - geocoder.js

## Folder explanation
Break down of each folder.
- controllers/ - Folder that contains all route files
- middleware/ - Folder that contains all middleware used by Express.js
- helpers/ - Folder to hold extra functions that would otherwise be on the global object. It can also be used to share functions between different parts of the project

## Controllers folder

### File Structure
Every folder, including the root controllers folder, must have a index.js file that allows a writer to include all routes inside the folder.  
Good:  
- **controllers/**
  - index.js
  - test.js
  - user/
    - index.js
    - dashboard.js  
    - settings/
      - index.js
      - settings_test.js
      - password.js

Good:
- **controllers/**
  - index.js
  - test.js
  - small-route.js
  - large-route/
    - index.js
    - large-route_test.js
    - start.js
    - middle.js
    - end.js

Bad:
- **controllers/**
  - long-route/
    - shorter-route/
      - end.js

Bad:
- **controllers/**
  - small-route.js
  - large-route/
    - start.js
    - middle.js
    - end.js   

### Routes
The name of a file or folder must reflex the route that it creates.  All parameter routes must be stored on the req

### Test Files
Tests are included in the folder that they are testing.  
All tests prepend the name of the folder to the test file name. So a folder named _maps_ would have a test file with the name *maps_test.js*



### folders
The folder name directly relates to the route that it creates.

## File naming
File names are always lowercase. If your file has multiple words in it, use a dash between (EG: `promise-handler.js`).
All JavaScript files must always have the extension .js.  
