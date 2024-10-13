Date: 12/10/2024

### How to use Netlify functions to hide API keys

When building web applications, it's crucial to keep sensitive information like API keys secure. Exposing these keys in your frontend JavaScript code can lead to misuse and security vulnerabilities. Netlify Functions provide a serverless solution to handle such sensitive data securely. In this learning post, we'll walk through how to use Netlify Functions to hide API keys in your JavaScript code.

### Why Use Netlify Functions?

Netlify Functions allow you to run server-side code without managing a server. This means you can securely handle API requests and keep your API keys hidden from the client-side code. Here’s a step-by-step guide on how to achieve this.

### Setup simple project

We will use simple project to fetch weather data from [Open Weather](https://openweathermap.org/). Please get your API key for fetching data from [Open Weather API](https://api.openweathermap.org/data/2.5/weather).

Follow steps in local setup guide of this [repository](https://github.com/krtEngineer/netlify_serverless_functions).

Here is functional code for Netlify function in this file [getWeatherData.js](https://github.com/krtEngineer/netlify_serverless_functions/blob/development/netlify/functions/getWeatherData.js)

```javascript
import dotenv from "dotenv";
import axios from "axios";

dotenv.config();

export const handler = async (event) => {
  try {
    const { city } = event.queryStringParameters;
    const baseUrl = process.env.WEATHER_API_BASE_URL;
    const appKey = process.env.WEATHER_API_KEY;
    const units = process.env.WEATHER_DATA_UNIT;
    const url = `${baseUrl}?q=${city}&appid=${appKey}&units=${units}`;
    let response = await axios.get(url);
    return {
      statusCode: 200,
      body: JSON.stringify({
        error: null,
        data: response.data,
      }),
    };
  } catch (error) {
    console.log(error.message);
    return {
      statusCode: 400,
      body: JSON.stringify({
        error: error.message,
        data: null,
      }),
    };
  }
};
```

Here is the functional code for using Netlify function in this file [index.js](https://github.com/krtEngineer/netlify_serverless_functions/blob/development/public/index.js)

```javascript
const button = document.querySelector("#btn");
const cityElement = document.querySelector("#city");
const tempElement = document.querySelector("#temperature");

button.addEventListener("click", async () => {
  city = "Pune";
  const response = await fetch(
    `/.netlify/functions/getWeatherData?city=${city}`
  );
  const data = await response.json();
  cityElement.innerText = data["data"]["name"];
  tempElement.innerText = `${data["data"]["main"]["temp"]}°C`;
});
```

Also add Netlify function configuration file [netlify.toml
](https://github.com/krtEngineer/netlify_serverless_functions/blob/development/netlify.toml)

```
[build]
	command = "# no command"
	functions = "netlify/functions"
	publish = "public"

[functions]
        node_bundler = "esbuild"
```

[Demo Application](https://krt-weather-api-serverless-fn.netlify.app/)

Result screenshot
![result](https://github.com/krtEngineer/TIL/blob/main/assets/02_image_2.png?raw=true)

Start using Netlify Functions today to enhance the security of your web applications!
