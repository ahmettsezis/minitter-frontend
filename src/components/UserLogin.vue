<template>
  <div class="login-container">
    <h1>Login</h1>
    <form @submit.prevent="login">
      <div>
        <label for="username">Username</label>
        <input type="text" id="username" v-model="username" required />
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" id="password" v-model="password" required />
      </div>
      <button type="submit">Login</button>
    </form>
    <p v-if="error" class="error">{{ error }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "", // Kullanıcı adını tutacak değişken
      password: "", // Şifreyi tutacak değişken
      error: null,  // Hata mesajlarını göstermek için
    };
  },
  methods: {
    async login() {
      try {
        // API'ye giriş isteği gönderiyoruz
        const response = await fetch("http://localhost:8080/login", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            username: this.username,
            password: this.password,
          }),
        });

        if (!response.ok) {
          throw new Error("Invalid credentials");
        }

        const data = await response.json();
        console.log("Login successful:", data);

        // Başarılı giriş sonrası işlemler (örneğin, token saklama)
        alert("Login successful!");
      } catch (error) {
        this.error = error.message; // Hata mesajını ekrana yansıtıyoruz
      }
    },
  },
};
</script>

<style scoped>
/* Basit stil eklemeleri */
.login-container {
  width: 300px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
.login-container h1 {
  text-align: center;
}
.login-container form div {
  margin-bottom: 15px;
}
.login-container label {
  display: block;
  font-weight: bold;
}
.login-container input {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  border: 1px solid #ddd;
  border-radius: 3px;
}
.login-container button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}
.login-container .error {
  color: red;
  text-align: center;
}
</style>
