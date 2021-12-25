<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input
            type="text"
            id="name"
            v-model="name"
            placeholder="digite seu nome: "
            autocomplete="off"
          />
        </div>
        <div class="input-container">
          <label for="bread">Escolha seu pão:</label>
          <select name="bread" id="bread" v-model="bread">
            <option value="">Selecione o seu pão</option>
            <option v-for="bread in paes" :key="bread.id" :value="bread.tipo">
              {{ bread.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Escolha sua carne:</label>
          <select name="meat" id="meat" v-model="meat">
            <option value="">Selecione sua carne</option>
            <option v-for="meat in carnes" :key="meat.id" :value="meat.tipo">
              {{ meat.tipo }}
            </option>
          </select>
        </div>
        <div id="options-container" class="input-container">
          <label id="options-title" for="meat">Selecione os opcionais</label>
          <div
            class="checkbox-container"
            v-for="options in optionsData"
            :key="options.id"
          >
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              :value="options.tipo"
            />
            <span> {{ options.tipo }} </span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu Hamburger" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "./Message";
export default {
  name: "BurgerForm",
  components: {
    Message,
  },
  data() {
    return {
      paes: null,
      carnes: null,
      optionsData: null,
      name: null,
      bread: null,
      meat: null,
      opcionais: [],
      msg: null,
    };
  },
  methods: {
    async getIgredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();
      this.paes = data.paes;
      this.carnes = data.carnes;
      this.optionsData = data.opcionais;
      console.log(data);
    },
    async createBurger(e) {
      e.preventDefault();
      const data = {
        name: this.name,
        meat: this.meat,
        bread: this.bread,
        options: Array.from(this.opcionais),
        status: "Solicitado",
      };
      const dataJson = JSON.stringify(data);
      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      this.msg = `Pedido nº ${res.id} realizado com sucesso!`;

      setTimeout(() => (this.msg = ""), 3000);
      
      this.name = "";
      this.meat = "";
      this.bread = "";
      this.opcionais = "";
    },
  },
  mounted() {
    this.getIgredients();
  },
};
</script>

<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
}
input,
select {
  width: 300px;
  padding: 5px 10px;
}
#options-container {
  flex-direction: row;
  flex-wrap: wrap;
}
.options-title {
  width: 100%;
}
.checkbox-container {
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}
.submit-btn {
  padding: 10px;
  margin: 0 auto;
  border: 2px solid #222;
  font-weight: bold;
  color: #fcba03;
  background: #222;
  cursor: pointer;
  transition: all 0.3s;
}
.submit-btn:hover {
  color: #222;
  background: transparent;
}
</style>
