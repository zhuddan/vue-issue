# vue

It's not working when i use kebab case props and function props in generic components

``` html
   <h2>It's not working </h2>
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
        name: {{ user.name }} == age: {{ user.age }} == isAdult: {{ user.isAdult }}
      </li>
    </CompKebabCase1>

    <h2>It's not working </h2>
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
        name: {{ user.name }} == age: {{ user.age }} == isAdult: {{ user.isAdult }}
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
        name: {{ user.name }} == age: {{ user.age }} == isAdult: {{ user.isAdult }}
      </li>
    </Comp>

```