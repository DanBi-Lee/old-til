# parcel과 모듈

## parcel과 모듈

1. `npm init -y`
2. `npm i parcel-bundler -D`
3. package.json

   > ```javascript
   > {
   >   "name": "catch-the-lion",
   >   "version": "1.0.0",
   >   "description": "",
   >   "main": "index.js",
   >   "scripts": {
   >     "dev" : "parcel index.html",
   >     "test": "echo \"Error: no test specified\" && exit 1"
   >   },
   >   "keywords": [],
   >   "author": "",
   >   "license": "ISC",
   >   "devDependencies": {
   >     "parcel-bundler": "^1.12.4"
   >   }
   > }
   > ```

4. index.html

   > ```markup
   > <!DOCTYPE html>
   > <html lang="en">
   > <head>
   >     <meta charset="UTF-8">
   >     <meta name="viewport" content="width=device-width, initial-scale=1.0">
   >   <title>Document</title>
   > </head>
   > <body>
   >     <script src="src/app.ts"></script>
   > </body>
   > </html>
   > ```

5. parcel 실행하면, 개발서버가 자동 실행.

