# Greg's Notes

# Greg's Setup steps:

1. `git clone https://github.com/zuletal/ImageLoader.git`
1. `cd ImageLoader`
1. `git checkout master`
1. `code .`
1. `cd server`
1. `npm install`
1. `npm install --save-dev nodemon`
   - nodemon will automatically reload our server when we make changes to its code. Without it, we need to stop the node process (using ctrl+C) and then restart it (with `npm start`)
1. Edit the file `server/package.json` and change the line `"start": "node ./bin/www"` to `"start": "nodemon ./app.js"`
   - the code from the tutorial has all the main code in `app.js`.  The code in `bin/www` clashes with `app.js`, so we don't need `bin/www` for this project.

# Greg's Running/Debugging Steps

1. Ran `npm start` and got an error because `mongoose` was not installed in this project - it was not listed in package.json
   - to install, use `npm install mongoose`
1. Ran `npm start` and got an error because `dotenv` was not installed in this project - it was not listed in package.json
   - to install, use `npm install dotenv`
1. Ran `npm start` and got an error because `multer` was not installed in this project - it was not listed in package.json
   - to install, use `npm install multer`
1. Ran `npm start` and got an error because `ejs` was not installed in this project - it was not listed in package.json
   - to install, use `npm install ejs`
1. Ran `npm start` and it complained about port 3000 being already in use:
   ```
   Server started
   Port 3000 is already in use
   ```
   But I know that port 3000 is not in use.  So I started reviewing the code in `app.js`.
   - I added comments indicating the code added from Step 1 and Step 2
   - I added a comment that the code from Step 3 is in `./models.js`
1. Ran `npm start`, browsed to `http://localhost:3000/` and after several seconds got an error in the server console:
   ```
   MongooseError: Operation `images.find()` buffering timed out after 10000ms
    at Timeout.<anonymous> (/Users/greg/nosync/ImageLoader/server/node_modules/mongoose/lib/drivers/node-mongodb-native/collection.js:184:20)
    at listOnTimeout (internal/timers.js:554:17)
    at processTimers (internal/timers.js:497:7)
   ```
1. Changed the URL in `app.js` for mongoose.connect() to use my own MongoDB (`mongodb://localhost/...`)
1. Ran `npm start`, browsed to `http://localhost:3000/` and saw the HTML page
1. Tried to upload an image and got an error: `Error: ENOENT: no such file or directory, open 'uploads/image-1610619310096'`
   - created a new directory `server/uploads`
1. IT WORKS!!!

# Most Significant Findings

1. The project code is great!  Well done!
1. To run the app, start `app.js` and not `./bin/www` (see step #7 in the first section above)
1. MongoDB was timing out with the given URL
1. Make sure a `uploads` directory exists


