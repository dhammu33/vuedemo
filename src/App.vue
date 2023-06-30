<template>
  <div>Hey {{ name }}</div>
  <div v-bind:class="isPromoted && 'promoted'">Spiderman</div>
  <div v-bind:class="[isPromoted && 'promoted', isSlodout ? 'soldout' : 'new']">
    Movie
  </div>
  <h2
    v-bind:class="{
      promoted: isPromoted,
      new: !isSlodout,
      soldout: isSlodout,
    }"
  >
    Conditional Movie
  </h2>
  <h1
    v-bind:style="{
      color: 'orange',
      fontSize: '50px',
    }"
  >
    Inline Style
  </h1>

  <h6 v-bind:style="styleObject">Style Object</h6>

  <h2 v-if="num === 0">Num 0</h2>
  <h1 v-else-if="num < 0">Negative</h1>
  <h1 v-else-if="num > 0">Positive</h1>
  <h2 v-else>Not Number</h2>

  <h2 v-show="showEle">v-show</h2>

  <!-- Array of String -->
  <h2 v-for="(name, index) in names" :key="name">{{ index }}{{ name }}</h2>

  <!-- Array of Objects -->
  <h1 v-for="name in fullNames" :key="name.first">
    {{ name.first }} {{ name.last }}
  </h1>

  <!-- Array of Arrays -->
  <div v-for="actor in actors" :key="actor.name">
    <h4>{{ actor.name }}</h4>
    <h3 v-for="movie in actor.movies" :key="movie">{{ movie }}</h3>
  </div>

  <h2 v-for="(value, key, index) in myInfo" :key="value">
    {{ index }} {{ key }} {{ value }}
  </h2>

  <template v-for="name in names" :key="name">
    <h1 v-if="name === 'Dhrumil'">{{ name }}</h1>
  </template>

  <h1>Add - {{ add(10, 10) }}</h1>
  <h1>Multiply - {{ multiply(10) }}</h1>

  <h6>{{ channel }}</h6>
  <div>
    <button v-on:click="channel = 'Dhammu'">Change Name</button>
    <!-- <button v-on:click="count +=1">Increment {{count}}</button> -->
  </div>
  <h3>{{ count }}</h3>
  <button v-on:click="increment(3, $event)">Increment</button>

  <button @:click="decrement(3)">Decrement</button>

  <h2>{{ channel }}</h2>
  <button v-on:click="changeName">Change Name</button>

  <div>
    <pre>{{ JSON.stringify(formValues, null, 2) }}</pre>
  </div>
  <form @submit.prevent="submitForm">
    <div>
      <label for="name">Name</label>
      <input type="text" id="name" v-model.trim.lazy="formValues.name" />
    </div>

    <div>
      <label for="profile">Profile</label>
      <textarea id="profile" v-model="formValues.profileSummary" />
    </div>

    <div>
      <label for="age">Age</label>
      <input type="number" id="age" v-model.number="formValues.Age" />
      <!-- <input @keyup.enter="submitForm" type="number" id="age" v-model.number="formValues.Age" /> -->
    </div>

    <div>
      <label for="country">Country</label>
      <select id="country" v-model="formValues.country">
        <option value="">Select a Country</option>
        <option value="India">India</option>
        <option value="Canada">Canada</option>
      </select>
    </div>

    <div>
      <label for="location">Location</label>
      <select id="location" multiple v-model="formValues.location">
        <option value="">Select a Country</option>
        <option value="India">India</option>
        <option value="Canada">Canada</option>
      </select>
    </div>

    <div>
      <input
        type="checkbox"
        id="remote"
        v-model="formValues.remoteWork"
        true-value="Yes"
        false-value="No"
      />
      <label for="remote">Open to remote work?</label>
    </div>

    <div>
      <label>Skill Sets</label>
      <br />
      <input
        type="checkbox"
        id="html"
        value="html"
        v-model="formValues.skillSets"
      />
      <label for="html">HTML</label>

      <input
        type="checkbox"
        id="css"
        value="css"
        v-model="formValues.skillSets"
      />
      <label for="css">CSS</label>

      <input
        type="checkbox"
        id="javascript"
        value="javascript"
        v-model="formValues.skillSets"
      />
      <label for="javascript">JAVASCRIPT</label>
    </div>

    <div>
      <label>Experience</label>
      <br />
      <input
        type="radio"
        id="0-2"
        value="0-2"
        v-model="formValues.experience"
      />
      <label for="0-2">0-2</label>

      <input
        type="radio"
        id="3-5"
        value="3-5"
        v-model="formValues.experience"
      />
      <label for="3-5">3-5</label>

      <input
        type="radio"
        id="6-10"
        value="6-10"
        v-model="formValues.experience"
      />
      <label for="6-10">6-10</label>
    </div>

    <div>
      <button>Submit</button>
    </div>
  </form>

  <!-- v-once directive -->
  <h1 v-once>{{ name }}</h1>
  <button @click="name = 'Spiderman'">Change Name</button>

  <!-- v-pre directive -->
  <h1 v-pre>{{ name }}</h1>

  <!-- computed Properties -->
  <!-- compose data from existing source -->
  <!-- chnage when their dependencies change -->

  <h2>{{ fullName }}</h2>
  <button @click="items.push({id:3,title:'Keyboard' ,price:700})"> Add </button>
  <h5>{{total}}</h5>
  <!-- computed Properties -->
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: "Dhrumil",
      firstName: "Dhrumil",
      lastName: "Gohil",
      count: 0,
      display: true,
      showEle: true,
      channel: "Dhrumil",
      isPromoted: true,
      isSlodout: true,
      styleObject: {
        color: "orange",
        fontSize: "50px",
      },
      num: 4,

      names: ["Dhrumil", "Yash", "Kartavya"],
      fullNames: [
        { first: "Dhrumil", last: "Gohil" },
        { first: "Yahs", last: "Patel" },
        { first: "Kartavya", last: "Chavda" },
      ],

      actors: [
        {
          name: "Christian Bale",
          movies: ["Batman", "The Prestige"],
        },
        {
          name: "Di Caprio",
          movies: ["Titanic", "Inception"],
        },
      ],
      myInfo: {
        name: "Dhrumil",
        course: "Vue",
      },
      multipler: 5,
      formValues: {
        name: "",
        profileSummary: "",
        country: "",
        location: [],
        remoteWork: false,
        skillSets: [],
        experience: "",
        Age: "",
      },
      items: [{ id: 1, title: "laptop", price: 5000 },
      { id: 2, title: "Phone", price: 2000 }],
    };
  },
  methods: {
    add(a, b) {
      return a + b;
    },
    multiply(a) {
      return a * this.multipler;
    },
    increment(num, event) {
      this.count += num;
      console.log("event", event);
    },
    decrement(num) {
      this.count -= num;
    },
    changeName(event) {
      this.channel = "Spiderman";
      console.log("event", event);
    },
    submitForm(event) {
      event.preventDefault();
      console.log("val", this.formValues);
    },
  },
  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`;
    },
    total(){
      return this.items.reduce((total,curr)=> (total = total + curr.price),0)
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}

.promoted {
  font-style: italic;
}

.soldout {
  color: red;
}

.new {
  color: green;
}
</style>
