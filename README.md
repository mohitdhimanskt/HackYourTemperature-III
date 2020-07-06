PROJECT: HackYourTemperature III

    This week you'll finish HackYourTemperature. Continue working from /homework/hackyourtemperature

This week we'll add our external API that we're going to work with: Open Weather Map. The goal this week is to learn how to make an API request from the backend, and then to send the result to the frontend.
4.1 The API

    We first have to make an account: do so via the website
    Go back to your project folder and create a new folder called sources. Inside create a file called keys.json. Go to your OpenWeatherMap account, find the API Key and copy it into keys.json

4.2 The Backend

    Remove the response from last week, we'll rewrite it later
    Inside of the the POST route, bring in axios and pass the value of the API endpoint: https://api.openweathermap.org/data/2.5/weather. For it to work we first have to add the API Key, like so:

const API_KEY = require('./sources/keys.json').API_KEY;
axios(`https://api.openweathermap.org/data/2.5/weather?APPID=${API_KEY}`);

Now, there are 2 situations that could happen: if the city name is not found, we want to send to the client a response with a message that the city isn't found. However, if the city is found and then we want to return a message that contains the city name and current temperature.

    If the result is not found, we render() to the page the index (just like in the / endpoint). However, also add a second argument, an object: { weatherText: "City is not found!" }
    If the result is found, we also render() to the page the index. Also add here the object. Only, instead of just a string dynamically add in the cityName and temperature (gotten from the result of the API call). Hint: use template strings to add variables in your strings!

4.3 The Frontend

In the frontend we're going to add one thing:

    Navigate to index.handlebars. Underneath the <form>, add a <p>. Give it the following content: {{ weatherText }} (Notice how the name weatherText refers back to the key in the object passed in the render())

Now test out your work to see if it behaves as expected. Run your server with node server.js. Open your browser at the right port and fill in the form. On submit there should appear a message underneath the form, that either says that the city isn't found or what the temperature is.