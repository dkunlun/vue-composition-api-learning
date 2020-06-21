<template>
    <div class="search">
        <button @click="increment">
            Ref is: {{ count }}
        </button>

        <button @click="add">
            Data is: {{ data }}
        </button>
    </div>
</template>

<script>
import { reactive, computed, ref, watchEffect, onMounted, toRefs } from '@vue/composition-api'

function useCount() {
    const count = ref(0)
    
    function increment() {
        count.value++
    }

    return {
        count,
        increment
    }
}

function useReactive() {
    const state = reactive({
        data: 0
    })

    function add() {
        state.data++
    }

    return {
        ...toRefs(state),
        add
    }
}

export default {
    setup() {
        const { count, increment } = useCount()
        const { data, add } = useReactive()
        return {
            count,
            increment,
            data,
            add
        }
    }
}
</script>