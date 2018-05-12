<template>
	<tr  :class="invite.status == 'read' ? 'table-success' : 'table-warning'">
	  <th scope="row">{{ invite.invite_id }}</th>
	  <td>{{ invite.sender_id }}</td>
	  <td>{{ invite.vector }}</td>
	  <td>{{ invite.status }}</td>
	  <td>{{ invite.invite }}</td>
	</tr>
</template>

<script>

export default {
  name: 'Notification',
  data () {
    return {
      data: null,
    }
  },
  props: ['invite']
}
</script>

<style scoped>
</style>
