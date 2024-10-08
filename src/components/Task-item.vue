<template>
  <li >
    <button><i class="far fa-circle"></i>{{ task.title }}</button>
    <button><i class="far fa-trash-alt"></i></button>
  </li>
</template>

<script>
export default {
  name: 'TaskItem',
  props:
    ['task'],
  
}
</script>