<template>
  <div class="dashboard">
    <TheHeader />
    <main>
      <TheToolbar />
      <TheTeam :users="users" />
    </main>
  </div>
</template>

<script>
import { ref } from 'vue';
import APIController from '@/controllers/api';

import TheHeader from '@/components/TheHeader.vue';
import TheToolbar from '@/components/TheToolbar.vue';
import TheTeam from '@/components/TheTeam.vue';
export default {
  name: 'App',
  components: {
    TheHeader,
    TheToolbar,
    TheTeam,
  },

  setup() {
    const users = ref([]);

    const fetchUsers = async () => {
      users.value = await APIController.FetchUsers();
    };

    return {
      users,
      fetchUsers,
    };
  },

  mounted() {
    this.fetchUsers();
  },
};
</script>

<style>
:root {
  --primary: #8a4cfc;
  --primary-alt: #702fe7;
  --light: #eeeeee;
  --light-alt: #f8f8f8;
  --grey: #888888;
  --dark: #131a26;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira sans', sans-serif;
}

body {
  background-color: var(--light);
}

main {
  width: 100vw;
  overflow: hidden;
}

input,
button {
  appearance: none;
  outline: none;
  border: none;
  background: none;
}

.button {
  display: inline-block;
  padding: 8px 16px;
  background-color: var(--primary);
  color: #fff;
  font-size: 20px;
  font-weight: 700;
  text-transform: uppercase;
  cursor: pointer;
  border-radius: 6px;
  transition: 0.4s;
}

.button:hover {
  background-color: var(--primary-alt);
}

.button.button-outline {
  background-color: transparent;
  border: 2px solid var(--primary);
  padding: 6px 14px;
  color: var(--primary);
}

.button.button-outline:hover {
  color: #fff;
  background-color: var(--primary);
}

.button.button-small {
  padding: 4px 8px;
  font-size: 18px;
  font-weight: 600;
}

.button.button-alert {
  background-color: crimson;
}

.button-group {
  display: flex;
  margin: 0 -8px;
}

.button-group.group-end {
  justify-content: flex-end;
}

.button-group .button {
  margin: 0 8px;
}
</style>
