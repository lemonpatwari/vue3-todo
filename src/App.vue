<template>
    <div class="container">
        <div class="col-lg-8 col-md-8 col-sm-12 offset-lg-2 offset-md-2">
            <div class="card box1">
                <div class="card-header">
                    Featured
                </div>

                <div class="card-header">
                    <form @submit.prevent="addToDo">
                        <input type="text" v-model="state.name" class="form-control" placeholder="Enter value">
                    </form>
                </div>
                <ul class="list-group list-group-flush">
                    <li v-for="(item,index) in state.items" class="list-group-item">

                        <div class="d-flex justify-content-between">
                            <div class="form-check">
                                <input class="form-check-input" @click="lineThrow(item.id)" type="checkbox" value=""
                                       :id="`flexCheckDefault${index}`">
                                <label class="form-check-label"
                                       :class=" item.status == false ? 'text-decoration-line-through' : ''"
                                       :for="`flexCheckDefault${index}`">
                                    {{ item.name }}
                                </label>
                            </div>

                            <div>
                                <button @click="deleteItem(index)">X</button>
                            </div>
                        </div>


                    </li>
                </ul>


                <div class="card-footer">
                    Item Left: {{ itemLeft }}
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>
.box1 {
    text-align: left;
}
</style>

<script>

import {computed, reactive} from "vue";

export default {
    name: 'App',

    setup() {
        const state = reactive({
            name: '',
            items: [
                {
                    id: 1,
                    name: 'lemon',
                    status: true,
                },

                {
                    id: 2,
                    name: 'lemon2',
                    status: true,
                },

                {
                    id: 3,
                    name: 'lemon3',
                    status: true,
                },
            ]
        })

        function addToDo() {
            let id = state.items.length;
            if (state.name == '') {
                alert('Enter name');
                return false;
            }
            state.items.push({
                id: parseInt(id) + 1,
                name: state.name,
                status: true
            });

            state.name = '';
        }

        function deleteItem(index) {
            state.items.splice(index, 1);
        }

        function lineThrow(id) {
            state.items.find(item => {
                if (item.id === id) {
                    item.status = !item.status;
                }
            })
        }

        const itemLeft = computed(()=>state.items.filter(item=> item.status).length)

        return {
            state,
            addToDo,
            deleteItem,
            lineThrow,
            itemLeft
        }
    },

}
</script>
