<template>
  <div class="auth-component">
    <b-form class="container container-auth">
      <b-form-group :label="siteId"></b-form-group>
      <b-form-input :placeholder="placeholder" :state="inputCheck" class="mb-3" v-model="input"></b-form-input>
      <b-alert class="mt-3" :show="alertCheck" variant="warning">Ошибка ввода id сайта</b-alert>
      <b-button type="submit" variant="primary" @click.prevent="submit">Войти</b-button>
    </b-form>
  </div>
</template>

<script>
const requestURL = "https://track-api.leadhit.io/client/test_auth";

export default {
  data() {
    return {
      input: "",
      placeholder: "Введите id",
      alert: false,
      siteId: "Leadhit-Site-Id"
    };
  },
  computed: {
    inputCheck: function() {
      if (this.input.length === 24) {
        return true;
      } else {
        return false;
      }
    },
    alertCheck: function() {
      if (this.alert === true && this.input.length === 0) {
        return true;
      } else {
        return false;
      }
    }
  },
  methods: {
    submit: function(event) {
      if (this.input.length !== 24) {
        this.alert = !this.alert;
        this.input = "";
        this.placeholder = "id сайта должен содержать 24 символа";
      } else {
        this.request(this.siteId);
      }
    },
    request: async function(siteId) {
      const id = siteId;
      await fetch(requestURL, {
        method: "GET",
        headers: {
          "Api-Key": "5f8475902b0be670555f1bb3:eEZn8u05G3bzRpdL7RiHCvrYAYo",
          [id]: "5f8475902b0be670555f1bb3"
        }
      }).then(response => {
        if (response.ok) {
          return response.json()
        } else {
          throw new Error('Invalid request')
        }
      }).then(data => {
        if (data.message === 'ok') {
          localStorage.setItem([id], '5f8475902b0be670555f1bb3')
          localStorage.setItem('key', true)
          this.$router.push('/stats')
        }
      });
    }
  }
};
</script>

<style lang="scss">
.container-auth {
  padding: 10px;
  border: 1px blue solid;
  border-radius: 10px;
}
</style>