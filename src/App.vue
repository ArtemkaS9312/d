
<template>
    <div id="app">
      <header>
        <h1>Sleeping Mood</h1>
      </header>
      
  
      <main class="boba">
        <div class="product-row" v-for="(product, index) in products" :key="index">
          <section class="product-card">
            <img :src=product.image :alt="product.name">
            <h2>{{ product.name }}</h2>
            <p>{{ product.description }}</p>
            <p>Количество: {{ product.quantity }}</p>
            <button type="button" @click="addToCart(index)">В корзину</button>
          </section>
        </div>
      </main>
  
      <div v-show="cart.length === 0" class="empty-cart">
        <p>Корзина пуста</p>
      </div>
  
      <div v-show="cart.length > 0" class="cart">
        <h2>Корзина</h2>В
        <ul>
          <li v-for="(item, index) in cart" :key="index">
            <p>{{ item.name }} <span class="quantity">{{ item.quantity }}</span></p>
            <button type="button" @click="removeFromCart(index)">Удалить</button>
          </li>
        </ul>
        <button type="button" @click="checkout">Купить</button>
      </div>
  
      <Add @add-product="addProduct"></Add>
  
      <footer>
        <p>© Sleeping Mood, 2023</p>
      </footer>
    </div>
  </template>




/* --------------------------------------------------------------------------------------------- */





<script>
import Add from './Add';

export default {
  components: {
    Add
  },
  data() {
    return {
      products: [
      { name: 'Rafl-2', description: 'Описание дивана 1. Здесь более подробное описание товара.', quantity: 5, image: require('./1.png') },
        { name: 'Loko PRO', description: 'Описание дивана 2. Здесь более подробное описание товара.', quantity: 13, image: require('./2.png') },
        { name: 'Carina Nova', description: 'Описание дивана 3. Здесь более подробное описание товара.', quantity: 8, image: require('./3.png') }
], 
      cart: [],
      showModal: false,
      newProduct: {
        name: '',
        description: '',
        quantity: ''
        
      }
    };
  },
  methods: {
    addToCart(index) {
      if (this.products[index].quantity > 0) {
        this.products[index].quantity--;
        const product = {
          name: this.products[index].name,
          quantity: 1
        };
        const existingProductIndex = this.cart.findIndex(item => item.name === product.name);
        if (existingProductIndex !== -1) {
          this.cart[existingProductIndex].quantity++;
        } else {
          this.cart.push(product);
        }
      }
    },
    removeFromCart(index) {
        const item = this.cart[index];
        const productIndex = this.products.findIndex(product => product.name === item.name);
        this.products[productIndex].quantity += 1; 
        item.quantity -= 1; 
        if (item.quantity === 0) { 
          this.cart.splice(index, 1);
        }
      },
      checkout() {
        if (this.cart.length > 0) {
          alert('Спасибо за покупку!');
          this.cart = [];
        }
      },
      addProduct(product) {
      this.products.push(product);
    },
    }
  };
</script>



/* --------------------------------------------------------------------------------------------- */


<style >
* {
  margin: 0;
  padding: 0;
}
.boba {
  margin-top: 8%; 
}
body {
  background: radial-gradient(circle at center, #FFFFFF 0%, #f7d1ba7d 100%);
  background-size: cover;
}




header {
    background-color: #f28749;
    color: #ffffff;
    text-align: center;
    padding: 40px;
  }
  
  main {    
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    flex-wrap: wrap;
    margin: 40px;
  }
  
  .product-card {
    border-radius: 30px;
    width: 300px;
    margin-bottom: 40px;
    padding: 20px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    text-align: center;
    background-color: #ffffffc7;
  }
  
  .product-card h2 {
    margin-top: 10px;
  }
  
  .product-card p {
    margin: 10px;
  }
  
  button {
    background-color: #e67e22;
    border: none;
    color: #fff;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    transition-duration: 0.4s;
  }
  
  button:hover {
    background-color: #d35400;
    color: #fff;
  }
  
  footer {
    position: fixed;
    bottom: 0;
    width: 100%;
    font-style: italic; 
    background-color: #0d6b90;
    color: #ffffff;
    text-align: center;
    padding: 20px;
  }
  
  /*----------------------Настройка корзины-------------------------*/
  
  .cart {
    color: #fff;
    position: fixed;
    top: 0;
    right: 0;
    width: 300px;
    height: 100%;
    background-color: 	 #b65822;
    box-shadow: 0 0 5px #3061699d; 
    padding: 20px;
  }
  
  .cart li {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-bottom: 10px;
  }
  
  .cart li p {
    margin: 0;
  }
  
  .cart li button {
    background-color: #e67e22;
    border: none;
    color: #fff;
    padding: 5px 10px;
    font-size: 14px;
    cursor: pointer;
    border-radius: 3px;
    transition-duration: 0.4s;
  }
  
  .cart li button:hover {
    background-color: #d35400;
    color: #fff;
  }
  
  .cart button {
    background-color: #e67e22;
    border: none;
    color: #fff;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: block;
    margin-top: 20px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    transition-duration: 0.4s;
  }
  
  .cart button:hover {
    background-color: #d35400;
    color: #fff;
  }
  
  .quantity {
    background-color: #cf793c;
    color: white;
    font-size: 16px;
    padding: 4px 8px;
    border-radius: 12px;
    margin-left: 8px;
  }


  .empty-cart {
    position: absolute;
    top: 50px;
    right: 20px;
    color: #f7d1ba;
    font-weight: bold;
    transition: 0.3s;
  }
  .empty-cart:hover {
    cursor: pointer;
    position: absolute;
    top: 50px;
    right: 20px;
    color: #fff;
    font-weight: bold; 
  }
  
  .empty-cart p {
    margin: 0;
  }


 

  
</style>