<template>
  <div class="container-fluid">
    <div class=" content d-flex justify-content-center">
      <div class="card rounded-5 bg-transparent px-5 pb-3">
      <form @submit.prevent="Login">
        <i class="bi bi-person-circle"></i>
        <div class="email my-2">
          <input v-model="email" type="email" class="form-control " id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="password mb-2" >
          <input v-model="password" type="password" class="form-control " id="exampleInputPassword1">
        </div>
        <button type="submit" class="btn btn-primary ">Kirim</button>
      </form>
    </div>
    </div>
  </div>
</template>
<style scoped>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css");
.container-fluid{
  background-color: rgb(0, 92, 148);
  height: 100vh;
}
i{
  font-size: 200px;
}
.card{
  margin-top: 13%;
}
</style>
<script setup>
definePageMeta({
  layout: 'login',
});
const supabase = useSupabaseClient();
const email = ref('');
const password = ref('');

const Login = async () => {
  const { data, error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  if (error) {
    alert('Password atau email Anda salah');
  } else {
    navigateTo('/');
  }
};
</script>