<template>
    <select class="my--select" :value="modelValue" @change="changeOption">
        <option disabled value="">Select from the list</option>
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
    color: rgb(101, 189, 101);
    border-radius: 10px;
    position: absolute; 
    top: 220px;  
    left: 300px;
    height: 50px;
    width: 150px;
    background: #4e565f;
}
</style>