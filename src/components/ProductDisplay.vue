<template>
  <main>
    <section id="product-section">
      <div class="product-container">
        <!-- Product details will be dynamically updated here -->
        <div v-if="isLoading" class="loader">
          <!-- Loader element -->
        </div>
        <div v-else>
          <div class="dividen">
            <div class="product_image">
              <img :src="product.image">
            </div>
            <div class="right">
            <div class="product_title">
              <h1>{{ product.title }}</h1>
            </div>
            <div class="product_category">
              <P class="category-p">{{ product.category }}</P>
              <div class="ellips-container">
                <p>2.9/5</p>
                <div class="boru">
                  <div class="ball full"></div>
                  <div class="ball full"></div>
                  <div class="ball full"></div>
                  <div class="ball no"></div>
                  <div class="ball no"></div>
                </div>
              </div>
            </div>
            <hr>
            <div class="product_description">
              <p class="description-p">{{ product.description }}</p>
            </div>
            <hr>
            <div class="product_price">
              <p class="price-p">${{ product.price }}</p>
            </div>
            <div class="button_container">
              <button @click="getBuyProduct" class="buy">Buy Product</button>
              <button @click="getNextProduct" class="next">Next Product</button>
            </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
  </template>
  <!-- <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script> -->
  <script>
  export default {
    name: "ProductDisplay",
    data() {
      return {
      apiUrl: 'https://fakestoreapi.com/products/',
      currentIndex: 1,
      product: {},
      isLoading: false
    }},
    created() {
      this.getNextProduct();
    },
    methods: {
      getNextProduct() {
        // Show loader
        this.isLoading = true;
  
        // Make API request
        fetch(this.apiUrl + this.currentIndex)
          .then(response => response.json())
          .then(data => {
            // Hide loader
            this.isLoading = false;
  
            // Update product details
            this.product = data;
          })
          .catch(error => {
            console.log('Error:', error);
            // Handle error scenario
          });
          
        // Increment index for the next product
        this.currentIndex++;
        if (this.currentIndex > 20) {
          this.currentIndex = 1;
        }
      },
      getBuyProduct() {
        this.isLoading = true;
        fetch(this.apiUrl + this.currentIndex)
          .then(response => response.json())
          .then(data => {
            // Hide loader
            this.isLoading = false;
  
            // Update product details
            this.product = data;
          })
          .catch(error => {
            console.log('Error:', error);
            // Handle error scenario
          });
      }
    }
  };
</script>
<style>
body {
  margin: 0px;
  padding: 0px;
  background-color: #ffffff;
}
.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
  display: flex;
  align-items: center;
  justify-content: center;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
.dividen {
  display: flex;
  width: 60%;
  height: 500px;
  background-color: #ffffff;
  padding: 15px;
  box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.75);
-webkit-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.75);
-moz-box-shadow: 0px 0px 24px 0px rgba(0,0,0,0.75);
  margin: 0px auto;
  margin-top: 50px;
}
.product-container {
  display: flex;
  width: 100%;
  height: 500px;
  background-color: #d6e6ff;
}
.product_image {
display: flex;
width: 70%;
height: 68%;
margin-top: auto;
margin-bottom: auto;
border-radius: 25px;
}
img {
  width: 100%;
  height: 85%;
  border-radius: 25px;
  margin-top: auto;
  margin-bottom: auto;
}
.right {
  margin: 20px;
}
.product_title {
display: block;
width: 100%;
height: 14.5%;
margin-bottom: 16px;
}
h1 {
  font-size: 1.5em;
  text-transform: capitalize;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 700;
  color: #002772;
}
.description-p {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1.1em;
  color: #1e1e1e;
}
.category-p {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 0.9em;
  font-weight: 300;
  color: #1e1e1e;
}
.price-p {
  font-size: 1.4em;
  font-family: Arial, Helvetica, sans-serif;
}
.product_category {
display: flex;
width: 99.2%;
height: 5%;
justify-content: space-between;
padding: 2px;
}
.ellips-container {
  display: flex;
  align-items: center;
  width: 40%;
  height: 100%;
  justify-content: right;
  gap: 5px;
}
.boru {
  display: flex;
  gap: 2px;
}
.ball {
  background-color: #002772;
}
.full {
  width: 20px;
  height: 20px;
  border-radius: 20px;
}
.no {
  width: 17px;
  height: 17px;
  border-radius: 20px;
  background-color: #ffffff;
  border: solid 2px #002772;
}
.product_price {
display: flex;
width: 100%;
height: 6%;
margin: 4px 0px;
}
.product_description {
  display: block;
  width: 100%;
  height: 45%;
}
.button_container {
  display: flex;
  width: 100%;
  height: 10%;
  justify-content: center;
  align-items: center;
  gap: 10px;
  padding: 4px 0px;
}
.next {
background-color: #ffffff;
border: 2px solid #002772;
border-radius: 7px;
}
.buy {
background-color: #002772;
border: 2px solid #002772;
border-radius: 7px;
color: #ffffff;
}
.button {
  width: 170px;
  height: 40px;
  font-size: 0.8em;
  font-weight: 900;
  text-transform: capitalize;
  color: #002772;
}
</style>