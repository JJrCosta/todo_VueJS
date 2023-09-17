<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaTarefas from './components/ListaTarefas.vue'

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
    {
      titulo: 'Exemplo de tarefa',
      finalizada: false
    },
    ],
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);
  }
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();  
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const novaTarefa = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(novaTarefa);
    estado.tarefaTemp = '';
  }

  const exibeMensagem = () => {
    if (getTarefasPendentes().length == 1) {
      return `Você possui ${getTarefasPendentes().length} tarefa pendente.`
    } else if (getTarefasPendentes().length){
      return `Você possui ${getTarefasPendentes().length} tarefas pendentes.`
    } else {
      return 'Você não possui tarefas pendentes'
    }
  }
</script>

<template>
  <div class="container">
    <Cabecalho :exibe-mensagem="exibeMensagem()"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaTarefas :tarefas = "getTarefasFiltradas()" />
  </div>
</template>