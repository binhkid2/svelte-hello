<script lang="ts">
    import axios from "axios";
    import { onMount, onDestroy, afterUpdate, beforeUpdate } from "svelte";
    import { fade, fly } from "svelte/transition";
  
    let products: {
        Description: string;
        Thumbnail: string ;
        Name:string
    }[] = [];
  
    const fetchData = async () => {
      const response = await axios.get(
        "https://sheet.best/api/sheets/e056296f-e82d-43f3-a913-5b4d3ed0ad95"
      );
      products = response.data;
    };
  
    onMount(() => {
      fetchData();
    });
  
   
  
 
  </script>
  
  <div class="container">
   
    <div class="photos">
      {#each products as product, i (product.Name)}
        <img
          src={product.Thumbnail}
          alt={product.Description}
          class="image"
          in:fly={{ y: 200, duration: 2000, delay: i * 200 }}
          out:fade
        />
      {/each}
    </div>
  </div>
  
  <style>
    .image {
      width: 400px;
      height: 250px;
      margin: 5px;
    }
    .photos {
      display: flex;
      flex-wrap: wrap;
    }
    .container {
      width: 1230px;
      margin: 0 auto;
    }
    .header {
      text-align: center;
      font-size: 20px;
    }
    .input {
      padding: 10px;
      width: 400px;
      border-radius: 10px;
      outline: none;
      border: 1px solid gray;
      font-size: 20px;
    }
    .button {
      padding: 10px;
      font-size: 20px;
      background-color: aqua;
      border-radius: 10px;
      border: none;
      color: white;
    }
    .input-container {
      margin-bottom: 40px;
    }
  </style>