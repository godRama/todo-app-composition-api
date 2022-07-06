<template>
    <div class="container mt-3">
        <div class="card">
            <div class="card-header">
                <div class="card-title text-center">Todo Application Composition API</div>
            </div>
            <div class="card-body">
                <div class="row">
                    <div class="col-9">
                        <input type="text" class="form-control" v-model="newEntry" @keyup.enter="add" />
                    </div>
                    <div class="col-3">
                        <button class="btn btn-success" @click="add">Add</button>
                    </div>
                </div>
                <ListTodo :listTodo="entry.list" @setStatus="setStatus" @delTodo="delTodo" />
            </div>
            <div class="card-footer">Total: {{ entry.list.length }}</div>
        </div>
    </div>
</template>

<script>
import { ref, reactive, onMounted } from "vue";
import ListTodo from "./components/ListTodo.vue";
export default {
    setup() {
        const newEntry = ref("");
        const entry = reactive({
            list: [],
        });

        onMounted(() => {
            const getItem = localStorage.getItem("myTodo1");
            entry.list = getItem ? JSON.parse(getItem) : [];
        });

        const add = () => {
            if (newEntry.value != "") {
                entry.list.unshift({
                    itemTodo: newEntry.value,
                    status: false,
                });
                newEntry.value = "";
            }
            saveToLocalStorage();
        };
        const setStatus = (indexTodo) => {
            entry.list = entry.list.filter((item, index) => {
                if (index == indexTodo) {
                    item.status = !item.status;
                }
                return item;
            });
            saveToLocalStorage();
        };
        const delTodo = (indexTodo) => {
            entry.list = entry.list.filter((item, index) => {
                if (index != indexTodo) {
                    return item;
                }
            });
            saveToLocalStorage();
        };
        const saveToLocalStorage = () => {
            localStorage.setItem("myTodo1", JSON.stringify(entry.list));
        };

        return {
            newEntry,
            entry,
            //method
            add,
            setStatus,
            delTodo,
        };
    },
    components: { ListTodo },
};
</script>
