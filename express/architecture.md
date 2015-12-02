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
The name of a file or folder must reflex the route that it creates.  All parameter routes must store some value that is required by a route on the Request object.

public.js
```Javascript
var router = module.exports = express.Router()
router //Creating basic route
  .route("/public")
  .get( function (req, res) ) {
    res.render("public")
  })
  .post( funciton (req, res) ) { 
    fs.save(req.file);
  })
  
  ...
  
router.param('file', function(req, res, next, file) { //Put the file on the Request object
  req.file = fs.readFileSync(file)
});

router //Creating route with parameter in it
  .route("/public/:file")
  .get( function (req, res) ) {
    res.send(req.file);
  })
  .post( function (req, res) ) {
    req.file = req.body.file
    req.file.save()
  })
```

### Test Files
Tests are included in the folder that they are testing.  
All tests prepend the name of the folder to the test file name. So a folder named _maps_ would have a test file with the name *maps_test.js*



### folders
The folder name directly relates to the route that it creates.  A folder with the path _./controllers/map_ must expose the route `/map`.

## Middleware Folder

## Folder structure

### Middleware Files
Middleware files will always return a middleware function.

```Javascript
module.exports = function (req, res next) {
  User
    .findById(req.params.id)
    .then( (user) => {
        req.user = user;
        next();  
    })
    .catch( (err) => {
      next(err);
    })
}
```
### Middleware folders
Middleware folders must be able to include all middleware inside the folder, and still return a middleware function.

```Javascript
module.exports = function(req, res next) {
  callFiles (filesInCurrentFolder)
}
```


## File naming
File names are always lowercase. If your file has multiple words in it, use a dash between (EG: `promise-handler.js`).
All Express.js Route files must always have the extension _.js_.  
