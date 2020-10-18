<template>
  <div>
    <header>
      <h1>{{ title }}</h1>
    </header>
    <div>
      <label for="lat">Latitude</label>
      <input type="text" v-model="lat" />
      <br />
      <label for="lon">Longitude</label>
      <input type="text" v-model="lon" />
      <br />
      <button v-on:click="getData">Submit</button>
    </div>
    <br />
    <div>
      <h4>Geo coordination</h4>
      Latitude:{{ lat2 }}<br />
      Longitude:{{ lon2 }}
    </div>
    <div>
      <h3>{{ currTitle }}</h3>
      <div>
        Temperatur: {{ temp }}<br />
        Humidity: {{ humi }}<br />
        Cloudiness: {{ clouds }}
      </div>
      <div>
        <h3>Current Day:</h3>
        Day Temperatur: {{ tempDay }}<br />
        Minimal Temperatur: {{ tempMin }}<br />
        Maximal Temperatur: {{ tempMax }}<br />
        Morning Temperatur: {{ tempMorn }}<br />
        Night Temperatur: {{ tempNight }}<br />
        Humidity:{{ humi0 }}<br />
        Cloudiness: {{ clouds0 }}
      </div>
    </div>
    <div>
      <h3>{{ forceastTitle }}</h3>
      <div>
        <h4>Day 1:</h4>
        Day Temperatur: {{ temp1 }}<br />
        Humidity:{{ humi1 }}<br />
        Cloudiness: {{ clouds1 }}
      </div>
      <div>
        <h4>Day 2:</h4>
        Day Temperatur: {{ temp2 }}<br />
        Humidity:{{ humi2 }}<br />
        Cloudiness: {{ clouds2 }}
      </div>
      <div>
        <h4>Day 3:</h4>
        Day Temperatur: {{ temp3 }}<br />
        Humidity:{{ humi3 }}<br />
        Cloudiness: {{ clouds3 }}
      </div>
      <div>
        <h4>Day 4:</h4>
        Day Temperatur: {{ temp4 }}<br />
        Humidity:{{ humi4 }}<br />
        Cloudiness: {{ clouds4 }}
      </div>
      <div>
        <h4>Day 5:</h4>
        Day Temperatur: {{ temp5 }}<br />
        Humidity:{{ humi5 }}<br />
        Cloudiness: {{ clouds5 }}
      </div>
      <div>
        <h4>Day 6:</h4>
        Day Temperatur: {{ temp6 }}<br />
        Humidity:{{ humi6 }}<br />
        Cloudiness: {{ clouds6 }}
      </div>
      <div>
        <h4>Day 7:</h4>
        Day Temperatur: {{ temp7 }}<br />
        Humidity:{{ humi7 }}<br />
        Cloudiness: {{ clouds7 }}
      </div>
    </div>
  </div>
</template>
<script>
const apiKey = "5fa04ff65f57916dd6c0f2d720a61d85";
const apiUrl = "https://api.openweathermap.org/data/2.5/onecall";

let lat = "48.210033";
let lon = "16.363449";

const data = {
  title: "Weather",
  loc: "Location: ",
  lat: lat, // default
  lon: lon, // default
  lat2: "",
  lon2: "",
  currTitle: "Current Weather",
  forceastTitle: "Forceast for next 7 Days",
  temp: "",
  humi: "",
  clouds: "",
  tempDay: "",
  tempMax: "",
  tempMin: "",
  tempMorn: "",
  tempNight: "",
  humi0: "",
  clouds0: "",
  temp1: "",
  humi1: "",
  clouds1: "",
  temp2: "",
  humi2: "",
  clouds2: "",
  temp3: "",
  humi3: "",
  clouds3: "",
  temp4: "",
  humi4: "",
  clouds4: "",
  temp5: "",
  humi5: "",
  clouds5: "",
  temp6: "",
  humi6: "",
  clouds6: "",
  temp7: "",
  humi7: "",
  clouds7: "",
};

async function getWeather(lat, lon) {
  const weatherurl =
    apiUrl +
    "?" +
    `lat=${lat}&` +
    `lon=${lon}&` +
    `units=metric&` +
    `exclude=hourly&` +
    `appid=${apiKey}`;
  const response = await fetch(weatherurl);
  const json = await response.json();
  return json;
}

async function getData() {
  const json = await getWeather(this.lat, this.lon);
  let temp = json.current.temp;
  let humi = json.current.humidity;
  let clouds = json.current.clouds;
  let Days = [];
  for (let i = 0; i < 8; i++) {
    Days[i] = json.daily[i];
  }

  (this.lat2 = json.lat),
    (this.lon2 = json.lon),
    (this.temp = temp),
    (this.humi = humi),
    (this.clouds = clouds),
    (this.tempDay = Days[0].temp.day),
    (this.tempMax = Days[0].temp.max),
    (this.tempMin = Days[0].temp.min),
    (this.tempMorn = Days[0].temp.morn),
    (this.tempNight = Days[0].temp.night),
    (this.humi0 = Days[0].humidity),
    (this.clouds0 = Days[0].clouds),
    (this.temp1 = Days[1].temp.day),
    (this.humi1 = Days[1].humidity),
    (this.clouds1 = Days[1].clouds),
    (this.temp2 = Days[2].temp.day),
    (this.humi2 = Days[2].humidity),
    (this.clouds2 = Days[2].clouds),
    (this.temp3 = Days[3].temp.day),
    (this.humi3 = Days[3].humidity),
    (this.clouds3 = Days[3].clouds),
    (this.temp4 = Days[4].temp.day),
    (this.humi4 = Days[4].humidity),
    (this.clouds4 = Days[4].clouds),
    (this.temp5 = Days[5].temp.day),
    (this.humi5 = Days[5].humidity),
    (this.clouds5 = Days[5].clouds),
    (this.temp6 = Days[6].temp.day),
    (this.humi6 = Days[6].humidity),
    (this.clouds6 = Days[6].clouds),
    (this.temp7 = Days[7].temp.day),
    (this.humi7 = Days[7].humidity),
    (this.clouds7 = Days[7].clouds);
}

export default {
  data() {
    return data;
  },
  methods: {
    getData: getData,
  },
};
</script>>