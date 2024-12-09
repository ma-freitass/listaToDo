<script setup>
//importar o ref(), deixa as variaveis reativas, onde conseguimos manipular os estados
import { ref } from "vue"
const tarefas = ref([])
//variavel para armazenar novas tarefas
const novaTarefa = ref("");

//verificar se novas tarefas já foram adicionadas
const jaAdicionouTarefa = ref(false);
//função para remover a tarefa
function removerTarefa(index) {
  tarefas.value.splice(index, 1)
  //remove o item pela posição clicada
}

//função para adicionar
function adicionarTarefa() {
  if (novaTarefa.value.trim() !== "") {
    tarefas.value.push(novaTarefa.value.trim())
    novaTarefa.value = "";
    jaAdicionouTarefa.value = true;
  }
}
</script>

<template>
  <section class="inicio">
    <h1> 📝 Lista de Tarefas</h1>
    <section class="novaTarefa">
      <input type="text" placeholder="Digite uma nova tarefa" v-model="novaTarefa">
      <!--a diretiva v-model ela sincroniza o valor de uma variável ao input-->
      <button class="adicionar"  @click="adicionarTarefa">Adicionar Tarefa</button>

      <p v-if="tarefas.length === 0 && !jaAdicionouTarefa">
        Você ainda não adicionou nenhuma tarefa 🤯
      </p>
      <p v-else-if="tarefas.length === 0 && jaAdicionouTarefa">
        🎉 Uhulll!! Você completou todas as tarefas! Parabéns!!
      </p>
    </section>


    <!--dentro da tag não precisa usar o value pq o vue já entende o que é reativo-->
    <section class="lista" v-if="tarefas.length > 0">

      <ul>
        <!--v-for é uma diretiva que serve para fazer loops, dentro do parenteses é passado o que eu quero que ele pegue no array, o item e a posição-->
        <li v-for="(tarefa, index) in tarefas" :key="index">{{ tarefa }}
          <button class="tarefaNova"  @click="removerTarefa(index)">✅</button>
        </li>
      </ul>
    </section>
  </section>
</template>

<style scoped lang="scss">
.inicio {
  width: 96vw;
  height: 90vh;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: "Montserrat", sans-serif;
  font-weight: 400;
  font-style: normal;
  background: linear-gradient(135deg, #bab3e4, #191970		);
  color: #ffffff;
}
h1{
  font-size: 1.9rem;
}
input, .adicionar{
  border-radius: 4px;
  border-style: none;
  width: 25vw;
  height: auto;
  display: flex; 
  align-items: center;
  text-align: center;
  justify-content: center;
  margin-bottom: 10px;
  
  font-size: 18px;
  color: #4837aa;
}
.adicionar{
  cursor: pointer;
  color: #080849;
}
ul{
  list-style: none;
  font-size: 1.5rem;
}
.tarefaNova{
  all: unset;
  cursor: pointer;
}
.novaTarefa{
  
  display: flex;
  width: 40vw;
  height: 15vh;
  flex-direction: column;
  margin: 20px 15px;
  padding: 20px;
  align-items: center;
  justify-content: center;
}
</style>