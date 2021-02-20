# boilerplate for nextjs - tailwind app

```
create-next-app appname
npm install tailwindcss autoprefixer @fullhuman/postcss-purgecss --save-dev
npx tailwindcss init -p
```

edit tailwind.config.js with following content
```
  module.exports = {
   purge: [],
   purge: ['./pages/**/*.{js,ts,jsx,tsx}', './components/**/*.{js,ts,jsx,tsx}'],
    darkMode: false, // or 'media' or 'class'
    theme: {
      extend: {},
    },
    variants: {
      extend: {},
    },
    plugins: [],
  }
```

include tailwind in css under styles folder
```
/* ./styles/globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```
Finally, ensure your CSS file is being imported in your `pages/_app.js` component:

#### Working with GraphQL
```
npm install @apollo/client graphql
```
check apollo docs for setup
v3 setup
```
import { ApolloClient, InMemoryCache } from '@apollo/client';
import { ApolloProvider } from '@apollo/client';

const client = new ApolloClient({
  uri: 'https://48p1r2roz4.sse.codesandbox.io',
  cache: new InMemoryCache()
});

function App() {
  return (
    <ApolloProvider client={client}>
      <div>
        <h2>My first Apollo app 🚀</h2>
      </div>
    </ApolloProvider>
  );
}
```
useQuery [docs](https://www.apollographql.com/docs/react/data/queries/)
```
import { useQuery, gql } from '@apollo/client';

const EXCHANGE_RATES = gql`
  query GetExchangeRates {
    rates(currency: "USD") {
      currency
      rate
    }
  }
`;

function ExchangeRates() {
  const { loading, error, data } = useQuery(EXCHANGE_RATES);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error :(</p>;

  return data.rates.map(({ currency, rate }) => (
    <div key={currency}>
      <p>
        {currency}: {rate}
      </p>
    </div>
  ));
}

```
useMutation [docs](https://www.apollographql.com/docs/react/data/mutations/)

#
# boilerplate for create-react-app - tailwind app

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

#### Add this to postcss.config.js
```
const purgecss = require("@fullhuman/postcss-purgecss")({
  content: ["./src/**/*.jsx", "./src/**/*.js", "./public/index.html"],
  css: ["./assests/tailwind.css"],
  // Include any special characters you're using in this regular expression
  defaultExtractor: (content) => content.match(/[A-Za-z0-9-_:/]+/g) || [],
});

module.exports = {
  plugins: [
    require("tailwindcss"),
    require("autoprefixer"),
    ...(process.env.NODE_ENV === "production" ? [purgecss] : []),
  ],
};
```
