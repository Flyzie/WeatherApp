<script>
export default{
    name: 'Header',
    props:{
        location: String,
    },
    methods:{
        updateLocation(event){
            this.$emit('update:location', event.target.value);
        }
    }
}
</script>

<template>
    <div class="container">
        <input  type="text" placeholder="Search Location: " :v-model="location" v-on:keyup.enter="updateLocation">
    </div>
</template>

<style scoped>

    input{
        
        border-radius: 20px;
        border: 0.2rem solid rgba(226, 226, 226, 0.5);
    }

</style>