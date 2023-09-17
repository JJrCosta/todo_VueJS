<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa" required>
            </div>
        </div>
        <div class="row mt-2 mb-2">
            <div class="d-grid gap-2 col-6 mx-auto">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col">
                <select @change="props.trocarFiltro" class="form-control text-center">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Tarefas Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>