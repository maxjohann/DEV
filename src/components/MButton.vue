<script setup>

const props = defineProps({
    texto: String
})

</script>

<template>
    <button>
        <slot>
            <m-button> {{ props.texto }} </m-button>
        </slot>
    </button>
</template>