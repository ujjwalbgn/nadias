<template>
    <div class="menu-item-list">
        <select v-model="categoryID" @change="fetchItems" required>
            <option value="">Select a category</option>
            <option v-for="cat in initialCategories" :value="cat.id" :key="cat.id">{{cat.name}}</option>
        </select>
        <ul>
            <li v-for="item in items" :key="item.id">
                <router-link :to="{name: 'edit-item', param: {id: item.id}}">
                    {{item.name}}
                </router-link>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: ['initialCategories'],
        data() {
            return {
                categoryID: this.initialCategories[0].id ,
                items : []
            }
        },
        created(){
          this.fetchItems();
        },

        methods: {
            fetchItems() {
                axios.get(`/api/categories/${this.categoryID}/items`)
                    .then(res => this.items  = res.data);
            }
        }
    }
</script>
