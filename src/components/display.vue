<template>
    <p class="font-bold text-3xl my-16">Display list</p>
    <div @click="getTodos" class="p-4 rounded cursor-pointer bg-blue-400 max-w-sm text-white w-28" >
        Refresh
    </div>

    <div class=" mx-auto grid lg:grid-cols-4 gap-6 sm:grid-cols-2 max-sm:grid-cols-1 p-8 ">
        <div v-for="item in items" class="border rounded bg-white p-4 ">
            <div class="flex justify-between items-center">
                <p class=" text-violet-400 p-3 rounded-md bg-slate-200">Featured</p>
                <p class="flex justify-center items-center h-8 w-8 border rounded-[50%] ">
                    <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 384 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M0 48C0 21.5 21.5 0 48 0l0 48V441.4l130.1-92.9c8.3-6 19.6-6 27.9 0L336 441.4V48H48V0H336c26.5 0 48 21.5 48 48V488c0 9-5 17.2-13 21.3s-17.6 3.4-24.9-1.8L192 397.5 37.9 507.5c-7.3 5.2-16.9 5.9-24.9 1.8S0 497 0 488V48z"/></svg>
                </p>
            </div>
            <div class="flex justify-between items-center mt-8">
                <img class="h-16 w-16 rounded-[50%] mx-auto" src="data:image/jpeg;base64,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" alt="">
            </div>
            <div class="text-center">
                <p class="text-xl font-medium">{{item.Name}}</p>
                <p class="font-light">{{item.jobtitle}}</p>
            </div>
            <div class="flex justify-between items-center">
                <p class="flex gap-2 items-center ">
                    <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 384 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M215.7 499.2C267 435 384 279.4 384 192C384 86 298 0 192 0S0 86 0 192c0 87.4 117 243 168.3 307.2c12.3 15.3 35.1 15.3 47.4 0zM192 128a64 64 0 1 1 0 128 64 64 0 1 1 0-128z"/></svg> <span>London </span>                   
                </p>
                <p class="flex gap-2 items-center ">
                    <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 320 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M160 0c17.7 0 32 14.3 32 32V67.7c1.6 .2 3.1 .4 4.7 .7c.4 .1 .7 .1 1.1 .2l48 8.8c17.4 3.2 28.9 19.9 25.7 37.2s-19.9 28.9-37.2 25.7l-47.5-8.7c-31.3-4.6-58.9-1.5-78.3 6.2s-27.2 18.3-29 28.1c-2 10.7-.5 16.7 1.2 20.4c1.8 3.9 5.5 8.3 12.8 13.2c16.3 10.7 41.3 17.7 73.7 26.3l2.9 .8c28.6 7.6 63.6 16.8 89.6 33.8c14.2 9.3 27.6 21.9 35.9 39.5c8.5 17.9 10.3 37.9 6.4 59.2c-6.9 38-33.1 63.4-65.6 76.7c-13.7 5.6-28.6 9.2-44.4 11V480c0 17.7-14.3 32-32 32s-32-14.3-32-32V445.1c-.4-.1-.9-.1-1.3-.2l-.2 0 0 0c-24.4-3.8-64.5-14.3-91.5-26.3c-16.1-7.2-23.4-26.1-16.2-42.2s26.1-23.4 42.2-16.2c20.9 9.3 55.3 18.5 75.2 21.6c31.9 4.7 58.2 2 76-5.3c16.9-6.9 24.6-16.9 26.8-28.9c1.9-10.6 .4-16.7-1.3-20.4c-1.9-4-5.6-8.4-13-13.3c-16.4-10.7-41.5-17.7-74-26.3l-2.8-.7 0 0C119.4 279.3 84.4 270 58.4 253c-14.2-9.3-27.5-22-35.8-39.6c-8.4-17.9-10.1-37.9-6.1-59.2C23.7 116 52.3 91.2 84.8 78.3c13.3-5.3 27.9-8.9 43.2-11V32c0-17.7 14.3-32 32-32z"/></svg>                     <span>23.30 </span>                   
                </p>
            </div>

        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { API } from 'aws-amplify';
import { listEmployees } from "./../graphql/queries";


let items = ref([]);


async function getTodos() {
  const result = await API.graphql({
    query: listEmployees
  });
  console.log(result);
  items.value = result.data.listEmployees.items;
}

getTodos(); // Call getTodos on component creation


</script>

<style lang="scss" scoped>

</style>