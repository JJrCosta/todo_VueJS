<script setup>
    const props = defineProps(['exibeMensagem']);
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p>
            {{ props.exibeMensagem }}
        </p>
    </header>
</template>