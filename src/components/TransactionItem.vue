<template>
    <ul>
        <li v-for="transaction in transactions" v-bind:key="transaction.id">
            <div>{{ transaction.created_at }}</div>
            <div>{{ transaction.description }}</div>
            <div>{{ transaction.amount }}</div>
        </li>
    </ul>        
</template>

<script>

export default {
    props: ['transactions'],    
}
</script>
