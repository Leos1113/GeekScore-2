<template>
  <the-dialog
    activator-icon="pencil"
    color="#fff"
    header="Edit team info"
    simple
    :submit-logic="onSubmit"
  >
    <v-text-field v-model="name" clearable :rules="nameRules" label="Name" />
    <v-switch v-model="toDelete" label="Delete team" color="error" hide-details />
  </the-dialog>
</template>

<script>
import { standardField } from "@/utils/validations";
import { mapActions } from "vuex";

export default {
  name: "TeamEditDialog",
  props: {
    team: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      name: this.team.name,
      toDelete: false,
      nameRules: standardField
    };
  },
  methods: {
    ...mapActions("teams", ["updateTeam", "deleteTeam"]),
    onSubmit() {
      if (this.toDelete) this.deleteTeam(this.team._id);
      this.updateTheTeam();
    },
    updateTheTeam() {
      const team = {
        _id: this.team._id,
        gameId: this.team.gameId,
        name: this.name
      };
      this.updateTeam(team);
    }
  }
};
</script>
