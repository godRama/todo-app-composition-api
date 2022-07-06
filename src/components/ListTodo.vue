<template>
    <div class="mt-4">
        <ul class="list-group">
            <li v-for="(item, i) in itemTodo" :key="i" class="list-group-item">
                <div class="row">
                    <div class="col-8">
                        <span v-if="item.status">
                            <del>{{ item.itemTodo }}</del>
                        </span>
                        <span v-else>
                            {{ item.itemTodo }}
                        </span>
                    </div>
                    <div class="col-2">
                        <button :class="[item.status ? 'btn-warning' : 'btn-primary', 'btn btn-sm']" v-html="item.status ? 'Cancel' : 'Done'" @click="setStatus(i)"></button>
                    </div>
                    <div class="col-2">
                        <button class="btn btn-sm btn-danger" @click="delTodo(i)">X</button>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import { toRefs } from "vue";
export default {
    props: {
        listTodo: {
            type: Array,
            default: [],
        },
    },
    setup(props, { emit }) {
        const { listTodo } = toRefs(props);
        const itemTodo = listTodo;
        console.log(itemTodo);

        const setStatus = (index) => {
            emit("setStatus", index);
        };
        const delTodo = (index) => {
            emit("delTodo", index);
        };

        return {
            itemTodo,

            //method
            setStatus,
            delTodo,
        };
    },
};
</script>
