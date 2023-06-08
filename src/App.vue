<script setup lang="ts">
import CompKebabCase1 from './components/CompKebabCase1.vue';
import CompKebabCase2 from './components/CompKebabCase2.vue';
import Comp from './components/Comp.vue';
interface UserModel {
  name: string;
  age: number; // age >=18 ==> adult
}

function getUserList() {
  return new Promise<UserModel[]>((resolve) => {
    resolve([
      {
        age: 17,
        name: 'aaa',
      },
      {
        age: 18,
        name: 'bbb',
      },
    ]);
  });
}

function isAdult(user: UserModel) {
  return {
    ...user,
    isAdult: user.age >= 18,
  };
}
</script>

<template>
  <div>
    <h2>don't work with kebab case props and inline function props</h2>
    <CompKebabCase1
      v-slot="{ list }"
      :data-fetch="getUserList"
      :formater="user => ({
        ...user,
        isAdult: user.age >= 18,
      })"
    >
      <li v-for="(user, index) in list" :key="index">
        <!-- Property 'isAdult' does not exist on type 'UserModel'.ts(2339) -->
        name: {{ user.name }} == age: {{ user.age }} == isAdult:{{ user.isAdult }}
      </li>
    </CompKebabCase1>
    
     <h2>don't work with kebab case props and inline function props</h2>
    <CompKebabCase2
      v-slot="{ list }"
      :fetch="getUserList"
      :data-formater="user => ({
        ...user,
        isAdult: user.age >= 18,
      })"
    >
      <li v-for="(user, index) in list" :key="index">
        <!-- Property 'isAdult' does not exist on type 'UserModel'.ts(2339) -->
        name: {{ user.name }} == age: {{ user.age }} == isAdult:{{ user.isAdult }}
      </li>
    </CompKebabCase2>

    <h2>work ！</h2>
    <Comp
      v-slot="{ list }"
      :fetch="getUserList"
      :formater="user => ({
        ...user,
        isAdult: user.age >= 18,
      })"
    >
      <li v-for="(user, index) in list" :key="index">
        name: {{ user.name }} == age: {{ user.age }} == isAdult:{{ user.isAdult }}
      </li>
    </Comp>

    <hr>

    <h2>work ！</h2>
    <CompKebabCase1
      v-slot="{ list }"
      :data-fetch="getUserList"
      :formater="isAdult"
    >
      <li v-for="(user, index) in list" :key="index">
        name: {{ user.name }} == age: {{ user.age }} == isAdult:{{ user.isAdult }}
      </li>
    </CompKebabCase1>

    <h2>work ！</h2>

    <CompKebabCase2
      v-slot="{ list }"
      :fetch="getUserList"
      :data-formater="isAdult"
    >
      <li v-for="(user, index) in list" :key="index">
        <!-- Property 'isAdult' does not exist on type 'UserModel'.ts(2339) -->
        name: {{ user.name }} == age: {{ user.age }} == isAdult:{{ user.isAdult }}
      </li>
    </CompKebabCase2>

    <h2>work ！</h2>
    <Comp
      v-slot="{ list }"
      :fetch="getUserList"
      :formater="isAdult"
    >
      <li v-for="(user, index) in list" :key="index">
        name: {{ user.name }} == age: {{ user.age }} == isAdult:{{ user.isAdult }}
      </li>
    </Comp>
  </div>
</template>

<style scoped>

</style>
