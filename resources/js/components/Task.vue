<template>
  <tr>
      <th scope="row">{{ index+1 }}</th>
      <td>{{ task.title }}</td>
      <td>{{ task.priority }}</td>
      <td><button class="btn btn-primary">Delete</button></td>
  </tr>
</template>

<script>
  export default {
    props: ['task', 'index']
  }
</script>

<style scoped>

</style>
