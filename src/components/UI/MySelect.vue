<template>
    <select class="my--select" :value="modelValue" @change="changeOption">
        <option value="">Sorting</option>
        <option 
            v-for="option in options" 
            :key="option.value" 
            :value="option.value"
            >
            {{ option.name }}
        </option>
    </select>
</template>

<script>
export default {
    name: 'my-select',
    props: {
        modelValue: {
            type: String
        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeOption(event) {
            this.$emit('update:modelValue', event.target.value); 
        }
    }
}
</script>

<style scoped>
.my--select{
    font-family: Oswald;
    color: var(--green, #38F2AF);
    border-radius: 10px;
    border: #373943;
    position: absolute; 
    top: 220px;  
    left: 300px;
    height: 50px;
    width: 150px;
    background: #373943;
}
</style>