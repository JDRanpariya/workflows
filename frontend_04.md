# Create boilerplate for react-tailwind app

- `create-react-app appname`

##
- `npm install tailwindcss postcss autoprefixer postcss-cli -D`

#### After installing the npm packages, now, you need to create a new folder inside src folder and name it assets and then inside the newly created assets folder create two files output.css and tailwind.css.
Open your tailwind.css file and paste the following code.
``` 
@tailwind base;
@tailwind components;
@tailwind utilities; 
```

#### create "tailwind.config.js" file and "postcss.config.js" file
- you can just do `npx tailwindcss init -p`

#### Now, open your package.json file and replace all the script files with these ones.
```  
"scripts": {
     "start": "npm run watch:css && react-scripts start",
     "build": "npm run watch:css && react-scripts build",
     "test": "react-scripts test",
     "eject": "react-scripts eject",
     "watch:css": "postcss src/assets/tailwind.css -o src/assets/output.css"
   }
```

#### Now, you need to import the output.css file inside your app.js file like this.
- import `'./assets/output.css'` And run `npm start`

#### Purge Css
- `npm i @fullhuman/postcss-purgecss`
