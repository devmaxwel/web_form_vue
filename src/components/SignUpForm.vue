<template>
  <form @submit.prevent="handleForm" @keydown.prevent.enter>
    <label>Email</label>
    <input type="email" required v-model="email" />
    <label>Password</label>
    <input type="password" required v-model="password" />
    <p class="error">{{ passwordError }}</p>
    <label>Select Role</label>
    <select v-model="role" required>
      <option value="designer">Web Design</option>
      <option value="developer">Web Development</option>
    </select>
    <label>Skils</label>
    <input
      type="text"
      @keyup="addSkill"
      v-model="isTemp"
      placeholder="Add skill and Press Enter"
    />
    <p class="error">{{ skillsError }}</p>

    <div v-for="skill in skilss" :key="skill" class="pis">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept Terms and Conditions</label>
    </div>
    <div class="submit">
      <button type="submit">Craete Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      isTemp: "",
      skilss: [],
      skillsError: "",
      passwordError: "",
    };
  },
  methods: {
    deleteSkill(skill) {
      this.skilss = this.skilss.filter((item) => skill !== item);
    },
    addSkill(e) {
      if (e.key === "Enter" && this.isTemp) {
        if (!this.skilss.includes(this.isTemp)) {
          this.skilss.push(this.isTemp.toLowerCase());
          this.skillsError = "";
          this.isTemp = "";
          return;
        } else {
          this.skillsError = "Skill already added";
        }
      }
    },
    handleForm() {
      this.passwordError =
        this.passwordError.length > 6 ? "" : "Password too is short";

      this.skillsError =
        this.skilss.length < 3 ? "you should add atleast three skills" : "";

      if (!this.passwordError && !this.skillsError) {
        console.log(this.skilss, this.email, this.password, this.role);

        return (
          (this.skilss = ""),
          (this.email = ""),
          (this.password = ""),
          (this.role = "")
        );
      }
    },
  },
};
</script>

<style>
form {
  max-width: 400px;
  margin: 30px auto;
  background: #fff;
  border-radius: 24px;
  padding: 40px;
  text-align: left;
}
input,
select {
  width: 80%;
  padding: 10px 6px;
  border-radius: 10px;
  outline: none;
  display: block;
  border: 1px solid gray;
}
label {
  display: block;
  padding: 10px 6px;
  text-transform: uppercase;
  font-weight: bold;
}
.terms {
  display: flex;
  justify-content: center;
  margin-top: 14px;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  position: relative;
  margin: 0 10px 0 0;
  top: 12px;
}
.submit {
  justify-content: center;
  display: flex;
}
.submit button {
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  background: rgb(109, 201, 109);
  color: #fff;
  outline: none;
  cursor: pointer;
}
.error {
  padding: 5px 0;
  color: #f00;
  margin: 0 5px;
}
.pis {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  color: #777;
  font-weight: bold;
  cursor: pointer;
}
</style>