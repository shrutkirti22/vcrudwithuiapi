<template>
    <div>
        <h1>Items</h1>

        <table class="table table-hover">
            <thead>
            <tr>
                <td>ID</td>
                <td>Item Name</td>
                <td>Item Price</td>
                <td>Actions</td>
            </tr>
            </thead>

            <tbody>
                <tr v-for="item in items" :key="item._id">
                    
                    <td>{{ item.name }}</td>
                    <td>{{ item.price }}</td>
                    <td><router-link :to="{name: 'Edit', params: { id: item._id }}" class="btn btn-primary">Edit</router-link></td>
                    <td><button class="btn btn-danger"  v-on:click="deleteItem(item._id)">Delete</button></td>
                </tr>
            </tbody>
        </table>

            </div>
</template>

<script>
    export default {
        data(){
            return{
                  perPage: 3,
        currentPage: 1,
        items: [
          { id: 1, first_name: 'Fred', last_name: 'Flintstone' },
          { id: 2, first_name: 'Wilma', last_name: 'Flintstone' },
          { id: 3, first_name: 'Barney', last_name: 'Rubble' },
          { id: 4, first_name: 'Betty', last_name: 'Rubble' },
          { id: 5, first_name: 'Pebbles', last_name: 'Flintstone' },
          { id: 6, first_name: 'Bamm Bamm', last_name: 'Rubble' },
          { id: 7, first_name: 'The Great', last_name: 'Gazzoo' },
          { id: 8, first_name: 'Rockhead', last_name: 'Slate' },
          { id: 9, first_name: 'Pearl', last_name: 'Slaghoople' }
        ]
                
            }
        },
        created: function()
        {
            this.fetchItems();
        },
        methods: {
            fetchItems()
            {
              let uri = 'http://localhost:4000/items';
              this.axios.get(uri).then((response) => {
                  this.items = response.data;
              });
            },
            deleteItem(id)
            {
              let uri = 'http://localhost:4000/items/delete/'+id;
              this.items.splice(id, 1);
              this.axios.get(uri);
            }
        }
    }
</script>