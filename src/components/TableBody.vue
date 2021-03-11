<template>
    <tr>
        <td>{{tableInfos.code}}</td>
        <td>{{tableInfos.name}}</td>
        <td>{{tableInfos.bid}}</td>
        <td>{{tableInfos.pctChange}}</td>
    </tr>  
</template>

<script>
export default {
    props: ['tableInfos']
}
</script>

<style scoped>
td{
    padding: 5px;
}
</style>