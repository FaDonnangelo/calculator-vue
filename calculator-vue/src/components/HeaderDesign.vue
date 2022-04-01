<template>
    <div class="headerBackground">
        <h1 id="title">Calculadora feita em Vue.js para a Aula 5</h1>
    </div>
</template>

<script>
export default {
    name: 'HeaderDesign',
    data(){ 

    },
    
}
</script>


<style scoped>
.headerBackground{
    background-color: cadetblue;
    width: 100%;
    height: 5%;
    min-height: 50px;
    float:inline-start;
    margin-bottom: 10px;
}

#title{
    color: black;
    margin-top: 0;
    font-family:fantasy;
    font-size: 40px;
    
}   
</style>