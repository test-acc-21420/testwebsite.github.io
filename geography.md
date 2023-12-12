<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Device Location</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f4;
    }

    header {
      background-color: #333;
      color: #fff;
      padding: 10px;
      text-align: center;
    }

    #main-container {
      max-width: 800px;
      margin: 20px auto;
      padding: 20px;
      background-color: #fff;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    #map {
      width: 100%;
      height: 400px;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <header>
    <h1>Device Location</h1>
  </header>
  <div id="main-container">
    <p>Click the button below to get your current geographic location:</p>
    <button onclick="getCurrentLocation()">Get Location</button>

    <div id="map"></div>
  </div>

  <script>
    function getCurrentLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition, showError);
      } else {
        alert("Geolocation is not supported by this browser.");
      }
    }

    function showPosition(position) {
      const latitude = position.coords.latitude;
      const longitude = position.coords.longitude;

      // Display the location on the map
      displayMap(latitude, longitude);
    }

    function showError(error) {
      let errorMessage = '';
      switch (error.code) {
        case error.PERMISSION_DENIED:
          errorMessage = "User denied the request for geolocation.";
          break;
        case error.POSITION_UNAVAILABLE:
          errorMessage = "Location information is unavailable.";
          break;
        case error.TIMEOUT:
          errorMessage = "The request to get user location timed out.";
          break;
        case error.UNKNOWN_ERROR:
          errorMessage = "An unknown error occurred.";
          break;
      }
      alert(errorMessage);
    }

    function displayMap(latitude, longitude) {
      const mapDiv = document.getElementById('map');

      // Create a Google Maps embed link
      const mapEmbedLink = `https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d${latitude}!2d${longitude}!3d${latitude}!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zNDDCsDE5JzU0LjIiTiAwwrAxMCcwMi45Ilc!5e0!3m2!1sen!2sus!4v1639290922907!5m2!1sen!2sus`;

      // Set the map as an iframe
      mapDiv.innerHTML = `<iframe width="100%" height="100%" frameborder="0" style="border:0" src="${mapEmbedLink}" allowfullscreen></iframe>`;
    }
  </script>
</body>
</html>
