<template>
  <div>
    <div id="app" v-if="info != null">
      <main>
        <app-header v-bind:info="info"></app-header>
        <forcast v-bind:dailyForcast="info.daily"></forcast>
      </main>
    </div>
    <div v-else class="data-loading">
      <p>Loading Weather app Data...</p>
    </div>
  </div>
</template>
<script>
import Header from "./components/Header.vue";
import Forcast from "./components/Forcast.vue";
export default {
  components: {
    "app-header": Header,
    forcast: Forcast
  },
  data() {
    return {
      info: null
    };
  },
  mounted() {
    fetch(
      "https://api.openweathermap.org/data/2.5/onecall?lon=2.159&lat=41.3888&uniots=metric&appid=ad86ce3ee764480409cf4761eedd5260"
    )
      .then(res => res.json())
      .then(data => {
        this.info = data;
      })
      .catch(err => console.log(err));
  }
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap");
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
main {
  background: linear-gradient(
    rgb(128, 202, 226),
    rgb(68, 68, 223),
    rgb(8, 8, 122)
  );
  color: white;
  max-width: 900px;
  width: 100%;
  margin: 2% auto;
  border-radius: 20px;
  padding: 2%;
  font-family: "Open Sans", sans-serif;
}
#app-header {
  display: flex;
  justify-content: space-between;
  margin: 0 auto 5% auto;
}
.current-info {
  width: 70%;
  margin: auto;
  p {
    font-size: 1.5rem;
  }
}

.current-icon {
  width: 20%;
  margin: auto;
}
.forcast {
  display: flex;
  justify-content: space-around;
  font-size: 1rem;
}
.eachDay {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.weather-icon {
  width: 50px;
  margin: 10% auto 10% auto;
}
.max-temp {
  color: rgb(197, 34, 34);
}
.min-temp {
  color: rgb(40, 230, 230);
}
@media screen and (max-width: 600px) {
  .forcast {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    font-size: 1rem;
  }
  .current-icon {
    width: 25%;
    margin: auto;
  }
  .current-info {
    width: 70%;
    margin: auto;
    p {
      font-size: 1rem;
    }
  }
  .eachDay {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    margin-top: 10px;
    margin-bottom: 10px;
    p {
      width: 10%;
    }
  }
  .weather-icon {
    width: 10%;
    margin: 0;
  }
}
@media screen and (max-width: 400px) {
  .current-icon {
    width: 30%;
    margin: auto;
  }
  .current-info {
    width: 65%;
    margin: auto;
    h1 {
      font-size: 1.5rem;
    }
    p {
      font-size: 1rem;
    }
  }
}
@media screen and (max-width: 290px) {
  .current-info {
    h1 {
      font-size: 1rem;
    }
    p {
      font-size: 0.5rem;
    }
  }

  .forcast {
    font-size: 0.5rem;
  }
  .eachDay {
    p {
      width: 20%;
      margin: 10px 0px;
    }
  }
  .weather-icon {
    width: 10%;
  }
}
</style>
