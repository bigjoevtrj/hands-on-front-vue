<template>
  <div>
    <div>
      <label>Nome</label>

      <input v-model="formList.name" placeholder="Digite o nome" />
    </div>

    <div>
      <label>Time</label>

      <input v-model="formList.team" placeholder="Digite o seu time" />
    </div>

    <button @click="addUser()">Cadastrar</button>

    <div v-for="(user, index) in users" :key="index">
      <p>Nome: {{ user.name }}</p>

      <p>Time: {{ user.team }}</p>

      <button @click="removeUser(user.id)">Remover</button>

      <button @click="editUser(user.id)">Editar</button>

      <hr />
    </div>
  </div>
</template>



<script lang="ts" setup>
import { ref } from "vue";

interface User {
  id?: number;

  name: string;

  team: string;

  sexuality: string;
}

const form = {
  name: "",

  team: "",

  sexuality: "",
};

const users = ref<User[]>([]);

const formList = ref<User>({ ...form });

function addUser() {
  users.value = [...users.value, { ...formList.value, id: +new Date() }];

  formList.value = { ...form };

  alert("User created");
}

function removeUser(id?: number) {
  if (!id) {
    alert("Please enter an id");

    return;
  }

  users.value = users.value.filter((user) => user.id !== id);

  alert("User removed");
}

function editUser(id?: number) {
  if (!id) {
    alert("Please enter an id");

    return;
  }

  const userEdited = users.value.find((user) => user.id === id);

  if (userEdited) {
    formList.value = { ...userEdited };

    users.value = users.value.filter((user) => user.id !== id);

    alert("User updated");
  }
}
</script>

