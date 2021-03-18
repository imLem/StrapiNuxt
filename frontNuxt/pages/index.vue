<template>
  <div>
    <div class="title">
      <h1>Hello World</h1>
    </div>
    <div class="container">
      <ul  class="max-w-sm rounded overflow-hidden shadow-lg p-1 mylist">
        <li v-for="item in filteredList" v-bind:key="item" class="px-6 py-4">
          <div class="font-bold text-xl mb-2">{{ item.name }}</div>
          <p
            class="text-gray-700 text-base"
          >{{ item.description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import itemsQuery from "~/apollo/queries/item/items";

export default {
  data() {
    return {
      items: [],
      query: ""
    };
  },
  apollo: {
    items: {
      prefetch: true,
      query: itemsQuery
    }
  },
  computed: {
    filteredList() {
      return this.items.filter(item => {
        return item.name.toLowerCase().includes(this.query.toLowerCase());
      });
    }
  }
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.mylist {margin: 0;padding: 0;list-style: none}
.mylist li {display: flex;flex-wrap: wrap;align-items: center;}
.mylist li p {margin-left: 15px;}
.mylist li + li {margin-top: 30px;}


.container {
  margin: 0 auto;
  min-height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  padding: top 1rem;
  text-align: center;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
