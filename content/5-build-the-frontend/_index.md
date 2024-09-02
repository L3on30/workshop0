+++
title = "Build the frontend"
date = 2020
weight = 5
chapter = false
pre = "<b>5. </b>"
+++


**Content:**
- [Install the Amplify Libraries](#install-the-amplify-libraries)
- [Style the App UI](#style-the-app-ui)
- [Implement the UI](#implement-the-ui)

#### Install the Amplify libraries
You will need two Amplify libraries for your project. The main aws-amplify library contains all of the client-side APIs for connecting your app's frontend to your backend, and the @aws-amplify/ui-react library contains framework-specific UI components.


1. **Open** a new terminal window, **navigate** to your projects root folder, and **run** the following command to install the libraries.

```bash
npm install aws-amplify @aws-amplify/ui-react
```

#### Style the app UI

1. On your local machine, navigate to the **`ai-recipe-generator/src/index.css`** file, and **update** it with the following code to center the App UI. Then, **save** the file.
```css
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color: rgba(255, 255, 255, 0.87);

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

}

.card {
  padding: 2em;
}

.read-the-docs {
  color: #888;
}

.box:nth-child(3n + 1) {
  grid-column: 1;
}
.box:nth-child(3n + 2) {
  grid-column: 2;
}
.box:nth-child(3n + 3) {
  grid-column: 3;
}
```

2. **Update** the **`src/App.css`** file with the following code to style the ingredients form. Then, **save** the file.

```css
.app-container {

  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.header-container {
  padding-bottom: 2.5rem;
  margin:  auto;
  text-align: center;

  align-items: center;
  max-width: 48rem;
  
  
}

.main-header {
  font-size: 2.25rem;
  font-weight: bold;
  color: #1a202c;
}

.main-header .highlight {
  color: #2563eb;
}

@media (min-width: 640px) {
  .main-header {
    font-size: 3.75rem;
  }
}

.description {

  font-weight: 500;
  font-size: 1.125rem;
  max-width: 65ch;
  color: #1a202c;
}

.form-container {
  margin-bottom: 20px;
}

.search-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
}

.wide-input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.search-button {
  width: 100%; /* Make the button full width */
  max-width: 300px; /* Set a maximum width for the button */
  padding: 10px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.search-button:hover {
  background-color: #0056b3;
}

.result-container {
  margin-top: 20px;
  transition: height 0.3s ease-out;
  overflow: hidden;
}

.loader-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.result {
  background-color: #f8f9fa;
  border: 1px solid #e9ecef;
  border-radius: 4px;
  padding: 15px;
  white-space: pre-wrap;
  word-wrap: break-word;
  color: black;
  font-weight: bold;
  text-align: left; /* Align text to the left */
}
```

#### Implement the UI

1. On your local machine, navigate to the **`ai-recipe-generator/src/main.tsx file`**, and **update** it with the following code. Then, **save** the file.

- The code will use the Amplify Authenticator component to scaffold out an entire user authentication flow allowing users to sign up, sign in, reset their password, and confirm sign-in for multifactor authentication (MFA).
```typescript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { Authenticator } from "@aws-amplify/ui-react";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <Authenticator>
      <App />
    </Authenticator>
  </React.StrictMode>
);
```

2. **Open** the **`ai-recipe-generator/src/App.tsx file`**, and **update** it with the following code. Then, **save** the file.
- The code starts by configuring the Amplify library with the client configuration file (amplify_outputs.json). It then generates a data client using the generateClient() function. The app presents a form to users for submitting a list of ingredients. Once submitted, it will use the data client to pass the list to the askBedrock query and retrieve the generated recipe then display it to the user.
```typescript
import { FormEvent, useState } from "react";
import { Loader, Placeholder } from "@aws-amplify/ui-react";
import "./App.css";
import { Amplify } from "aws-amplify";
import { Schema } from "../amplify/data/resource";
import { generateClient } from "aws-amplify/data";
import outputs from "../amplify_outputs.json";


import "@aws-amplify/ui-react/styles.css";

Amplify.configure(outputs);

const amplifyClient = generateClient<Schema>({
  authMode: "userPool",
});

function App() {
  const [result, setResult] = useState<string>("");
  const [loading, setLoading] = useState(false);

  const onSubmit = async (event: FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    setLoading(true);

    try {
      const formData = new FormData(event.currentTarget);
      
      const { data, errors } = await amplifyClient.queries.askBedrock({
        ingredients: [formData.get("ingredients")?.toString() || ""],
      });

      if (!errors) {
        setResult(data?.body || "No data returned");
      } else {
        console.log(errors);
      }

  
    } catch (e) {
      alert(`An error occurred: ${e}`);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="app-container">
      <div className="header-container">
        <h1 className="main-header">
          Meet Your Personal
          <br />
          <span className="highlight">Recipe AI</span>
        </h1>
        <p className="description">
          Simply type a few ingredients using the format ingredient1,
          ingredient2, etc., and Recipe AI will generate an all-new recipe on
          demand...
        </p>
      </div>
      <form onSubmit={onSubmit} className="form-container">
        <div className="search-container">
          <input
            type="text"
            className="wide-input"
            id="ingredients"
            name="ingredients"
            placeholder="Ingredient1, Ingredient2, Ingredient3,...etc"
          />
          <button type="submit" className="search-button">
            Generate
          </button>
        </div>
      </form>
      <div className="result-container">
        {loading ? (
          <div className="loader-container">
            <p>Loading...</p>
            <Loader size="large" />
            <Placeholder size="large" />
            <Placeholder size="large" />
            <Placeholder size="large" />
          </div>
        ) : (
          result && <p className="result">{result}</p>
        )}
      </div>
    </div>
  );
}

export default App;
```

3. **Open** a new terminal window, **navigate** to your projects root directory, and **run** the following command to launch the app:  
```bash
npm run dev
```

4. Choose the **Create Account** tab, and use the authentication flow to create a new user by entering **your email address** and a **password**. Then, choose **Create Account**.

![Image](/images/5-build-the-frontend/createaccount.png?width=20pc)

5. You will get a verification code sent to your email. Enter the **verification code** to log in to the app.

![Image](/images/5-build-the-frontend/wemail.png?width=20pc)

6. When signed in, you can start **inputting ingredients**

![Image](/images/5-build-the-frontend/meetyour.png?width=30pc)

And **generating recipes** by clicking to **generate** button. 

![Image](/images/5-build-the-frontend/generate.png?width=30pc)

7.  In the open terminal window, **run** the following command to push the changes to **GitHub**: 
```bash
git add .
git commit -m 'connect to bedrock'
git push origin main
```
8. **Sign in** to the AWS Management console in a new browser window, and **open** the AWS Amplify console at [AWS Amplify](https://console.aws.amazon.com/amplify/apps).

9. AWS Amplify automatically builds your source code and deployed your app at **https://...amplifyapp.com**, and on every git push your deployment instance will update.

- Select the **Visit deployed URL** button to see your web app up and running live.
![Image](/images/5-build-the-frontend/ai-recipe.png?width=30pc)
