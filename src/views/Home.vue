// HTML PART OF DOCUMENT
<template>
  <body>
    <div id="map" v-on:click="addOrder">click here</div>
    <header>
      <center>
        <h1>Welcome to BoorgirHeaven Online!</h1>
      </center>
    </header>
    <main class="document">
      <section class="burgers">
        <h2>Select Burger</h2>
        <p>This is where you execute burger selection</p>
        <center>
          <div>
            <Burger
              v-for="burger in burgers"
              v-bind:burger="burger"
              v-bind:key="burger.name"
            />
          </div>
        </center>
      </section>
      <section class="delivery">
        <h2>Customer Information</h2>
        <p>This is where you provide necessary information</p>
        <p>
          <label for="firstname">Full Name</label><br />
          <input
            type="text"
            id="firstname"
            name="fn"
            required="required"
            placeholder="First and Last name"
          />
        </p>
        <p>
          <label for="E-mail address">Email</label><br />
          <input
            type="text"
            id="E-mail address"
            name="ln"
            placeholder="E-mail Adress"
          />
        </p>
        <p>
          <label for="street">Street</label><br />
          <input
            type="text"
            id="street"
            name="st"
            required="required"
            placeholder="Street name"
          />
        </p>
        <p>
          <label for="house">House</label><br />
          <input
            type="text"
            id="house number"
            name="hn"
            required="required"
            placeholder="House number"
          />
        </p>
        <p>
          <label for="recipient">Payment Options</label><be></be><br />
          <select id="recipient" name="rcp">
            <option>Credit Card</option>
            <option>Swish</option>
            <option>Klarna</option>
            <option>Cash</option>
          </select>
        </p>
        <p>
          <label for="gender">Gender</label><br />
          <input
            type="radio"
            id="gender"
            name="ge"
            required="required"
            placeholder="gender"
          />Male<br />
          <input
            type="radio"
            id="gender"
            name="ge"
            required="required"
            placeholder="gender"
          />Female<br />
          <input
            type="radio"
            id="gender"
            name="ge"
            required="required"
            placeholder="gender"
          />Other
        </p>
      </section>
      <section>
        <button type="submit">
          <img
            src="https://www.seekpng.com/png/full/382-3823176_check-box-outline-tick-box-icon.png"
            alt="Span"
            title="Another in-line element"
            style="width: 10px"
          />
          Place my order!
        </button>
      </section>
    </main>
    <footer>
      <br />
      <hr />
      <p>© 2022 Hypothetical Burgers Inc.</p>
    </footer>
  </body>
</template>

<!-- JAVASCRIPT PART OF DOCUMENT  -->
<script>
import Burger from "../components/Burger.vue";
import io from "socket.io-client";
import burgerArray from "../views/menu.json"
const socket = io();

// function MenuItem( nam, url, kCa, glu, lac){
//   this.name = nam;
//   this.url = url;
//   this.kCal= kCa;
//   this.gluten= glu;
//   this.lactose= lac;
// }


// PRINT ARRAY OF BURGERS
console.log(burgerArray);

export default {
  name: "Home",
  components: {
    Burger,
  },
  data: function () {
    return {
      burgers: burgerArray,
    };
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random() * 100000);
    },
    addOrder: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top,
      };
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: {
          x: event.clientX - 10 - offset.x,
          y: event.clientY - 10 - offset.y,
        },
        orderItems: ["Beans", "Curry"],
      });
    },
  },
};
</script>

// CSS PART OF DOCUMENT 
<style>
header {
  background: url("https://c.tenor.com/lw7KNVchBmUAAAAC/burgir-meme.gif");
  color: white;
  -webkit-text-fill-color: white; /* Will override color (regardless of order) */
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: black;
  margin: 5px 20px;
  padding: 50px;
  border: 5px solid black;
}

body {
  font-family: arial;
  font-size: 18px;
}

.burgers {
  border: 10px double white;
  padding: 20px;
  color: #ffffff;
  background-color: black;
}

.delivery {
  border: 1px dashed black;
  padding: 20px;
}

#ingredient {
  font-weight: 1000;
}

.burger {
  margin: 0 20px;
  padding: 10px;
}

button {
  margin: 40px 0 0 0;
}

button:hover {
  background-color: #95ff9f;
  box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
    0 17px 50px 0 rgba(0, 0, 0, 0.19);
  cursor: pointer;
}

section {
  margin: 5px 20px;
}
</style>