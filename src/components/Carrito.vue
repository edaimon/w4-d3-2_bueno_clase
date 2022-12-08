<template>
  <!-- Crear el carrito -->
  <button @click="fetchApi">Obten Carrito</button>
  <form action="" @submit.prevent="validateForm()">
    <table>
      <thead>
        <tr>
          <th>index</th>
          <th>name</th>
          <th>photo</th>
          <th>price</th>
          <th>quantity</th>
          <th>total</th>
        </tr>
      </thead>
      <!--    {
            "uuid":"3",
            "name":"Vectorify",
            "description":"User Experience Design",
            "content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
            "image":"https://github.com/ironhack-jc/mid-term-api/blob/main/3.jpg?raw=true",
            "purshased_at":"June 10, 2021",
          "price": 5.50,
          "quantity":1,
          "active": true
        }, 
   -->
      <tbody>
        <tr v-for="(item, index) of items" :key="index">
          <td>{{ index }}</td>
          <td>{{ item.name }}</td>
          <td><img :src="item.image" :alt="item.name" width="70" /></td>
          <td>{{ item.price }}€</td>
          <td>
            <button @click="decrementQuantity(item)" type="button">-</button>

            <input
              type="number"
              v-model.number="item.quantity"
              placeholder="0"
            />

            <button @click="++item.quantity" type="button">+</button>
          </td>
          <td>{{ priceLine(item) }}€</td>
        </tr>
      </tbody>

      <tfoot>
        <tr>
          <th colspan="6">Total: {{ total }}€</th>
        </tr>
      </tfoot>
    </table>
    <button type="submit">Confirmar compra</button>
  </form>
</template>

<script>
export default {
  props: ["items", "total"],
};
</script>