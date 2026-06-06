# plant-whisperer
A website where each time you visit, it generates a poetic message based on the real-time weather in your city — like ‘The rain whispers to the succulent: you’re not alone.’ Uses your IP to fetch local weather and turns it into lyrical, whimsical micro-poetry.

This code gets weather condition of your location
```js
async function getWeather(latitude, longitude) {
    const url = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=weather_code`;
    const response = await fetch(url);
    const data = await response.json();
    const weathercode = data.current.weather_code;
    generatePoem(weathercode);
}
```

Following is the js code for generating poems according to the weather
```js
function generatePoem(code) {
    let poem = ""
    if (code === 0) {
        poem = "The sunflower looks up to the clear blue sky, relaxing in the warmth of the sunlight."
    }

    else if (code >= 1 && code <= 3) {
        poem = "The fern swings gently in the breeze, enjoying the cool shade of the clouds."
    }

    else if ([45, 48, 51, 53, 55, 56, 57].includes(code)) {
        poem = "The rain taps on the leaves, nourishing the soil and refreshing the plants with its gentle touch."
    }

    else if ([71, 73, 75, 77, 85, 86].includes(code)) {
        poem = "The snow covers the ground in a soft white blanket, while the roots sleep beneath the frozen earth."
    }

    else if([85,96,99].includes(code)){
        poem = "Thunder rumbles in the sky, shaking the leaves and the plants."
    }

    else{
        poem = "The unpredictable weather is reflecting the mood of the plants, as they dance in the beauty of nature's ever-changing creations."
    }

    document.getElementById("message").innerText = poem
}
```
This script finds your city/town/village/country and displays it
```js
async function getCity(latitude, longitude) {
    const response = await fetch(`https://geocode.maps.co/reverse?lat=${latitude}&lon=${longitude}&api_key=(Your_API_key)&accept-language=en`)
    const data = await response.json()
    console.log(data)
    document.getElementById("city").innerText = data.address?.city || data.address?.town || data.address?.village || data.address.country || "Location could not be found!"
}
```
