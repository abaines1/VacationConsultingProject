# Portfolio Project: Marriott Bonvoy Hotels and Villas

## Contents

- Introduction
- Provided Code
- Deliverable

## Introduction
With your product research finished and your priorities established, it's time to write some code. 

When the page loads, users will be greeted with a popup modal that asks them where they want to go - "city", "beach", or "mountains". When the user selects an option, the modal will disappear and the page should generate a list of recommended destinations. Your task is to write the logic that will select and render recommendations to the page as cards in the "Recommendations" section and text in the "Destinations" dropdown. 

There are plenty of comments and scaffolding to help you get the job done in `script.js`. Keep in mind that the tasks in the Deliverable section build upon each other so **you should complete each task in order!**

> **🗒 Note:** The only file you'll need to code in to complete this project is `script.js`.

## Provided Code

**`PLACES`** - This is an array that lives in the `places.js` file. Go ahead and examine it to see what each place object looks like. Each place has properties that you'll use for filtering.

**`centerPlaceOnMap(placeName)`** - This function works with the Mapbox API to pan the map to a selected location. 

## Deliverable

### Task 0 - **`mapboxgl.accessToken`**

You'll need to go to the Mapbox website and [sign up for an API key](https://account.mapbox.com/auth/signup/). It's a free service and you can call on your map 50,000 times a month! If you can't sign up for your own key, ask the HelpHub and they can provide you with one temporarily.

Once you have your key, add it between the quotes. It should look something like this:

```js
mapboxgl.accessToken = "pk.eyJ1IjoiZGFuNXpThisIsNotARealTokenTNrcWdreGhpNmVkdyJ9.1QGM2sWs-dwc5r8RiG1-VN";
```

<hr>

### Task 1 - **`filterPlacesByType(typePreference)`**

| Parameter        | Type   | Example Argument |
| ---------------- | ------ | ---------------- |
| `typePreference` | String | `"beach"`        |

This function should return a filtered array of places based off the user's type preference.

You'll filter the `PLACES` array by comparing the `type` of each place with the argument supplied to the `typePreference` parameter. The function should return a new array of filtered places.

<hr>

### Task 2 - **`createCard(place)`**

| Parameter   | Type   | Example Argument |
| ----------- | ------ | ---------------- |
| `place`     | Object | `{name: "Algarve", location: "Portugal", long: -7.93044, lat: 37.019356, img: "assets/images/popular-destinations/algarve.jpg", type: "beach"}`|

This function accepts a single place object as an argument. It should create a Bootstrap column containing a card for the specified `place` using DOM manipulation and return it. 

To make sure the card is styled properly and integrates with the provided Mapbox API logic, the column should have the same structure as the HTML below. Take special note of the card's `onclick` attribute. It calls the included `centerPlaceOnMap` function that pans the map to the selected location. Be sure pass it the name of the place whose card you're creating. 


```html 
<div class="col">
  <div class="card h-100" onclick="centerPlaceOnMap(place.name)">
    <img src="..." class="card-img-top h-100" alt="...">
    <div class="card-body">
      <h5 class="card-title">place.name</h5>
      <p class="card-text">place.location</p>
    </div>
  </div>
</div>
```

To test your logic, call the function from your console and pass in an object from `PLACES`. You should see the column and card elements displayed in your console.

> **Note:** This can be easily accomplished with template literals. To learn more about creating HTML elements with template literals, check out [this awesome article from Wes Bos.](https://wesbos.com/template-strings-html)

<hr>

### Task 3 - **`populateRecommendationCards(filteredPlaces)`**

| Parameter        | Type  | Example Argument |
| ---------------- | ----- | -----------------|
| `filteredPlaces` | Array | `[{name: "Algarve", location: "Portugal", long: -7.93044, lat: 37.019356, img: "assets/images/popular-destinations/algarve.jpg", type: "beach"}, {name: "Bali", location: "Indonesia", long: 115.188919, lat: -8.409518, img: "assets/images/popular-destinations/bali.jpg", type: "beach", }, ...]` |

This function accepts a filtered array of place objects as an argument (e.g. all places with the type "beach"). To start, find the DOM element with the id "recommendations" and clear it out. 

Next, you'll need to loop through `filteredPlaces` and use the  `createCard` function you wrote in task 2 to create DOM elements for each place object.

Finally, you'll append each created card to the "recommendations" div to populate the "Recommended for You" section.

<hr>

### Task 4 - **`findPlaceByName(placeName)`**

| Parameter   | Type   | Example Argument |
| ----------- | ------ | ---------------- |
| `placeName` | String | `"Bali"`         |

This function should find an object in `PLACES` where the object's `name` property matches the argument passed to the `placeName` parameter. It's used to pin our place on the interactive map and fly to it when clicked from the dropdown menu or the "Recommended for You" section.

To do this, you'll loop through the array of `PLACES` and look for a place object where the `name` property is the same as `placeName`. The function should return that place object.
