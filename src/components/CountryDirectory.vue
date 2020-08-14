<template>
  <div class="container">
    <h1>{{ title }}</h1>
    <form>
      <label for="country">Select a Country: </label>
            <select id="country" @change='selectedCountry($event)' v-model="details.country">
               <option :value="country.name" v-for="country in countries" :key="country.id">{{ country.name }}</option>
            </select>

     <label for="state">Select a State: </label>
            <select id="state" @change='selectedState($event)' v-model="details.state">
              <option :value="state.name" v-for="state in states" :key="state.id">{{ state.name }}</option>
            </select>
          <span v-if="noState">No known state available</span>

    <label for="city">Select a City: </label>
            <select id="city" v-model="details.city">
              <option :value="city.name" v-for="city in cities" :key="city.id">{{ city.name }}</option>
            </select>
            <span v-if="noCity">No known city available</span>
    </form>
    <div class="details">
      <h4>County: <span v-if="details.country"> {{ details.country }}</span> </h4>
      <h4>State: <span v-if="details.state"> {{ details.state }} </span> </h4>
      <h4>City: <span v-if="details.city"> {{ details.city }} </span> </h4>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      title: 'Country Directory App',
      countries: [],
      states: [],
      cities: [],
      details: {
        country: '',
        state: '',
        city: ''
      },
      noState: false,
      noCity: false
    }
  },
  created() {
    fetch("https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries%2Bstates%2Bcities.json", {
      method: "GET"
    })
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        this.countries = jsonData;
      });
  },
  methods: {
    selectedCountry(e) {
      const countryValue = e.target.value
      const country = this.countries.findIndex(e => e.name === countryValue)
      const state = this.countries[country]['states'];

      if(state.length == " "){
        this.noState = true
      }else{

      this.states = state
      }

    },
    selectedState(e) {
      const stateValue = e.target.value
      const state = this.states.findIndex(e => e.name === stateValue)
      const city = this.states[state]['cities'];

      if(city.length == " "){
        this.noCity = true
      }else{
        this.cities = city
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  background: rgb(219, 2, 45);
  border: 2px white;
  width: 450px;
  height: 600px;
  margin: auto;
  top: 30px;
  position: relative;
  border-radius: 0 10px;
}

h1{
    color: #ffffff;
    text-align: center;
    font-weight: lighter;
    padding: 10px 20px;
}

form{
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  padding: 10px 20px;
}

label{
  font-size: 1rem;
  color: #fff;
  margin: 10px 0;
}

select{
  height: 30px;
  outline: none;
  font-family: inherit;
  border: 1px solid transparent;
  border-radius: 1px;
  cursor: text;
}
.details {
  backdrop-filter: blur(100px);
  padding: 10px 20px;
}
.details h4 {
  font-weight: 400;
  color: #fff;
}
span{
  font-weight: 400;
  color: #fff;
}
@media screen and (max-width: 768px) {
  .container {
    width: 350px;
  }
  }
</style>
