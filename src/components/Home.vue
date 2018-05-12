<template>
  <div class="container home">
  <p v-if="!updated">Data will be updated after 5 seconds</p>
  <h2 class="text-center" v-if="!updated">INVITATIONS</h2>
  <h2 class="text-center" v-if="updated">UPDATED INVITATIONS</h2>
    <table class="table table-hover">
      <thead>
        <tr>
          <th scope="col">ID</th>
          <th scope="col">Sender</th>
          <th scope="col">Vector</th>
          <th scope="col">Status</th>
          <th scope="col">Invite</th>
        </tr>
      </thead>
      <tbody>
        <Notification :key="i.invite_id" :invite="i" v-for="i in invitations" />
      </tbody>
    </table>
  </div>
</template>

<script>
import Invitations from '../data/invitations.json'
import InvitationsUpdate from '../data/invitations_update.json'
import Notification from './Notification'

export default {
  name: 'Home',
  data () {
    return {
      invitations: Invitations.invites,
      invitationsUpdate: InvitationsUpdate.invites,
      updated: false
    }
  },
  components: { Notification },
  created() {
    setTimeout(() => {
       this.getUpdates();
       this.updated = true;
    }, 5000);
  },
  methods: {
    getUpdates() {
      this.invitationsUpdate.forEach(iu => {
        let changed = false;
        this.invitations.forEach((i, index) => {
          if (iu.invite_id === i.invite_id) {
            this.invitations[index] = iu;
            changed = true;
          }
        })

        if (!changed) {
          this.invitations.push(iu);
        }
      });
    }
  }
}
</script>

<style scoped>
</style>