<template>
    <div class="search">
        <button @click="increment">
            Ref is: {{ count }}
        </button>

        <button @click="add">
            Data is: {{ data }}
        </button>

        <Demo @click.native="use"></Demo>
    </div>
</template>

<script>
import { reactive, computed, ref, watchEffect, onMounted, toRefs } from '@vue/composition-api'
import Demo from '@/components/Demo'

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

        function use() {
            console.log(123)
        }

        return {
            count,
            increment,
            data,
            add,
            use
        }
    },
    components: {
        Demo
    }
}
</script>