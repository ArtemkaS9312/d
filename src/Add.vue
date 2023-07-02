<template>
    <div>
      <button type="button" class="add3" @click="showModal = true">Добавить</button>
      <div v-show="showModal" class="modal">
        <div class="modal-content">
          <span class="close" @click="showModal = false">&times;</span>
          <h2>Добавить новый товар</h2>
          <form @submit.prevent="addNewProduct">
            <label for="name">Название:</label>
            <input type="text" id="name" v-model="newProduct.name" required>
            <label for="description">Описание:</label>
            <input type="text" id="description" v-model="newProduct.description" required placeholder="Описание дивана. Здесь более подробное описание товара.">
            <label for="quantity">Количество:</label>
            <input type="number" id="quantity" v-model="newProduct.quantity" required>
            <label for="image">Изображение (150x150):</label>
            <input type="file" id="image" ref="fileInput" @change="onFileChange">
            <img v-if="newProduct.image" :src="newProduct.image" alt="Изображение">
            <button type="submit">Сохранить</button>
            <button type="button" @click="showModal = false">Отмена</button>
          </form>
        </div>
      </div>
    </div>
  </template>




  /*-----------------------------------------------*/


  <script>
  export default {
    data() {
      return {
        showModal: false,
        newProduct: {
          name: '',
          description: '',
          quantity: '',
          image: ''
        }
      };
    },
    methods: {
      onFileChange(event) {
        const file = event.target.files[0];
        if (file) {
          this.newProduct.image = URL.createObjectURL(file);
        }
      },
      addNewProduct() {
        this.$emit('add-product', { ...this.newProduct });
        this.newProduct.name = '';
        this.newProduct.description = '';
        this.newProduct.quantity = '';
        this.newProduct.image = '';
        this.showModal = false;
      }
    }
  };
  </script>


/*-----------------------------------------------*/


<style scoped>

form {
    display: flex;
    flex-direction: column;
  }
  
  label {
    font-weight: bold;
    margin-bottom: 5px;
  }
  
  input[type="text"],
  input[type="number"],
  textarea {
    border: none;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  input[type="text"]:focus,
  input[type="number"]:focus,
  textarea:focus {
    outline: none;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }
  
  button[type="submit"] {
    background-color:#e67e22;
    color: white;
    border: none;
    margin-top: 12px;
    margin-bottom: 10px;
    border-radius: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }
  
  button[type="cancel"] {
    background-color: #e67e22;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }
  
  img {
    max-width: 150px;
    max-height: 150px;
    margin-bottom: 20px;
  }

  .modal {
    display: flex;
    position: fixed;
    z-index: 9999;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    align-items: center;
    justify-content: center;
  }
  
  .modal-content {
    background-color: #fff;
    padding: 40px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    max-width: 600px;
    min-width: 300px;
    max-height: 90%;
    overflow-y: auto;
  }
  .close {
    cursor: pointer;
  }

  .add3 {
    position: absolute;
    top: 40px;
    left: 20px;
    z-index: 9999;
  }
</style>