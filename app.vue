<script setup>
const requestContent = ref({
  'hello': 'world'
})

const logContent = ref([])

const send = () => {
  $fetch('/api/ping', {
    method: 'POST',
    body: requestContent.value,
  })
  logContent.value.push(new Date().toISOString() + ' sent.')
}
</script>

<template>
  <div>
    <pre>{{ JSON.stringify(requestContent) }}</pre>

    <button @click="send">Send Request</button>

    <ul>
      <li v-for="log in logContent">{{ log }}</li>
    </ul>
  </div>
</template>
