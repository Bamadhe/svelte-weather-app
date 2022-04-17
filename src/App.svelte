<script>

	const openweather_id = "97a9f94b48e4088640647b297a2f11e9";
	const bingmaps_id = "Ao7uoQbYVpz3_dvtjG453FuI_o-hrj4cagewsgeQofnRkjGY3Xkv-c9Pb6lqhkYd";
	var city_name = "";
	var temperature = "";
	var temp_min = "";
	var temp_max = "";
	var wind_speed = "";
	var humidity = "";
	var weather_status = "";
	var map = "";
	var receivedData = null;
  
	
	  async function loadData(){
	  const response = await fetch(`http://api.openweathermap.org/data/2.5/weather?q=${city_name}&APPID=${openweather_id}&units=metric`)
	  if(response.ok){
	  receivedData = await response.json()
	  console.log(receivedData);
	  temperature = receivedData.main.temp;
	  humidity = receivedData.main.humidity;
	  temp_min = receivedData.main.temp_min;
	  temp_max = receivedData.main.temp_max;
	  wind_speed = receivedData.wind.speed;
	  weather_status = receivedData.weather[0].description;
	  map = `https://dev.virtualearth.net/REST/v1/Imagery/Map/Road/${receivedData.coord.lat},${receivedData.coord.lon}/12?centralpoint=${receivedData.coord.lat},${receivedData.coord.lon};&dcl=1&mapSize=1000,500&mapLayer=TrafficFlow&key=${bingmaps_id}`;
	}
  }
  
</script>
  
  <style>

	.main {
	  text-align: center;
	}

	.title {
	  text-align: center;
	}

	button {
	  background-color: #f6d55c;
	}

	.data {
	  text-align: center;
	}
  
	.list {
	  width: 50%;
	  text-align: left;
	  margin-left: 25%;
	  border-style: ridge;
	  border-color: #f6d55c;
	}
	
	img {
  	  border: 3px solid #f6d55c;
	}
  
  </style>

	<div class="title">
  		<img src="/title.png" alt="NoPictureToShow" />
	</div>

  	<div class="main">
	<input bind:value={city_name}  placeholder="Enter a city name in English">
	<button on:click={loadData}>Check Weather</button>
  
	{#if receivedData != null}
	  <div class="data">
		<div class="list">
		  <table style="width:100%">
		  <tr>
			<td>Temperature:</td>
			<td><span>{temperature}&deg</span></td>
			<td>Maximum Temperature:</td>
			<td><span>{temp_max}&deg</span></td>
		  </tr>
		  <tr>
			<td>Humidity:</td>
			<td><span>{humidity}%</span></td>
			<td>Minimum Temperature:</td>
			<td><span>{temp_min}%</span></td>
		  </tr>
		  <tr>
			<td>Weather Status:</td>
			<td><span>{weather_status}</span></td>
			<td>Wind Speed:</td>
			<td><span>{wind_speed}km/h</span></td>
		  </tr>
		  </table>
		</div>
		<img src={map} alt="NoPictureToShow" />
	  </div>
	{/if}
  </div>
