
<script setup>
import ItemsLayout from './ItemsLayout.vue';


defineProps({
    items: Array
});

// kebab-case is the recommended naming convention for emit  
const emit = defineEmits(["add-to-cart"]);

function addToCart(item) {
    emit ("add-to-cart", item);
    console.log(item.name + " event emitted from the child");
}

</script>

<template>
    <div>
        <h1>Our Products</h1>
        <ul>
            <!---
            <ItemsLayout v-for="item in items" :key="item.id">
            {{ item.name }}  {{  item.price }} {{ item.img }}
            </ItemsLayout> -->

            <ItemsLayout v-for="item in items" :key="item.id">

            <template v-slot:image>
                <img :src="item.img" :alt="item.name" class="menuImg">
            </template>

            <template #title>
                {{ item.name }}
            </template>

            <template v-slot:price>
                €{{ item.price }}
            </template>

            <template v-slot:actions>
                <button @click="addToCart(item)">Add to cart </button>
            </template>
        </ItemsLayout>
        </ul>
    </div>
</template>


<style scoped>
.container {
    background-color: #999;
    padding: 20px;
    color: black;
}

ul {
    padding: 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
}

.menuImg {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    border: 2px solid brown;
    margin-bottom: 10px
}

.menuImg:hover {
    border: 4px solid brown;
}
</style>