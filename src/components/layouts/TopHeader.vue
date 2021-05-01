<template>
    <header>
        <h1>{{ title}}</h1>
    </header>
</template>
<script>
export default {
    props:['title']
}
</script>

<style scoped>
header{
    width: 100%;
    height: 4rem;
    background: linear-gradient( to bottom right ,#fa8e00, #f6d5a9);
    background-color: #fa8e00;
    display: flex;
    justify-content: center;
    align-items: center;
}
header h1 {
  color: rgb(0, 0, 0);
  margin: 0;
}
</style>