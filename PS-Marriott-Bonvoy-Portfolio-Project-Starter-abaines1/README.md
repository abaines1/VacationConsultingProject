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


### Task 5 - **`swal()`**
Utilize the SweetAlert library to display a modal dialog when the page loads. The modal dialog presents the user with a question, "Where do you want to go?" and offers three buttons labeled "City," "Beach," and "Mountains." Each button corresponds to a travel preference category.

When the user clicks on one of these buttons, the value associated with the button is captured. This value represents the user's preference for the type of travel destination selected.

After capturing the user's preference, it assigns the value to the typePreference variable. Subsequently, it calls the `findRecommendations(typePreference)` function, passing the user's preference as an argument.

The closeOnClickOutside: false option ensures that the modal dialog remains open until the user makes a selection, preventing accidental dismissal by clicking outside the dialog.

### Task 6 - **`const map = new mapboxgl.Map()`**
Initialize a Mapbox map on the web page. It relies on the Mapbox GL JS library, which requires a valid access token to function correctly.

The new `mapboxgl.Map({ ... })` constructor creates a new map object with the following configuration options:

`container`: Specifies the HTML element ID where the map should be rendered. It targets an element with the ID "map," indicating that the map will be displayed within that specific container on the page.
`style`: Specifies the map's visual style using a mapbox style URL
`zoom`: Determines the initial zoom level of the map. 
`center`: Sets the initial geographic coordinates (longitude and latitude) where the map should be centered.

### Task 7  - **`findRecommendations(type)`**
This function findRecommendations(type) is responsible for generating recommendations based on a specified type (e.g., "City," "Beach," "Mountains") provided as an argument.

It calls the `filterPlacesByType(type)` function to filter the places array based on the given type, which returns an array of filtered places stored in filteredPlaces.
If filteredPlaces is not empty (if (filteredPlaces)), the function proceeds to perform the following actions for each place in filteredPlaces:a. Adds the place to a megamenu using the addPlaceToMegaMenu(place) function.b. Adds a card to the "Recommended for You" section, likely using a function called populateRecommendationCards(filteredPlaces) to populate the UI with relevant information about each place.c. Creates a marker on the map for each place using the addMarkerToMap(place) function.
If filteredPlaces is empty (which indicates an error in the filtering process), an error message is logged to the console indicating the issue.

### Task 8 - **`centerPlaceOnMap(placeName)`**
This function centerPlaceOnMap(placeName) is designed to move the map's view to a specific place based on its name, enhancing the user's navigation experience.

It calls the `findPlaceByName(placeName)` function to locate the object representing the specified place within the PLACES array. The resulting place object is stored in the variable placeObj.
If placeObj is not null or undefined (if (placeObj)), indicating that the place was successfully found, the function proceeds to perform the following actions:
  a. Scrolls the page to the map element using document.getElementById("map").scrollIntoView() to ensure the map is in view.
  b. Utilizes the Mapbox GL JS library's map.flyTo({ ... }) method to smoothly transition the map's center to the coordinates [placeObj.long, placeObj.lat]. These coordinates are likely retrieved from the placeObj representing the selected place.
If placeObj is null or undefined (which could happen if the specified place name is not found in the PLACES array), an error message is logged to the console.

### Task 9 - **`addPlaceToMegaMenu(place)`**
Define DOM nodes _megaMenuCol1 and _megaMenuCol2, representing two columns in a megamenu interface on the web page.

The `addPlaceToMegaMenu(place)` function is responsible for dynamically adding a new place item to the megamenu.

It constructs an HTML list item (li) with an onclick event that calls the `centerPlaceOnMap('${place.name}')` function when clicked. 

Inside the list item, an anchor (a) element with a class of "dropdown-item" displays the place name (${place.name}).
The menuItemContent variable holds this HTML structure.
The function checks the number of child elements in _megaMenuCol1. If it's less than 4 (indicating there's space for another item), the new menu item HTML (menuItemContent) is appended to _megaMenuCol1 using insertAdjacentHTML("beforeend", menuItemContent).
If _megaMenuCol1 is already full (i.e., it has 4 or more child elements), the new menu item is added to _megaMenuCol2 in a similar manner.

### Task 10 - **`addMarkerToMap(place)`**
This function addMarkerToMap(place) is responsible for placing a Mapbox marker on the map at the coordinates specified by the place object.

It creates a new mapboxgl.Popup object with an offset of 25 pixels and sets its HTML content to include the place name (${place.name}) and an image

Then inserts an image tag into the popup's HTML content. The image source (src) is set to the URL specified in place.img. The style attribute adjusts the image's width to 200 pixels, ensures its height adjusts accordingly, and adds a border-radius of 4 pixels for a rounded appearance.

It creates a new mapboxgl.Marker object with a black color and sets its geographic coordinates (setLngLat) to [place.long, place.lat], which are the longitude and latitude values of the place.
The marker's popup is set using setPopup(popup) with the previously created popup containing the place's information.
Finally, the marker is added to the map using addTo(map).