<template>
  <div>
    <div class="container">
      <div class="wrapper">
        <h2>Hitung Umur</h2>
        <div class="card">
          <div class="form-group">
            <VueDatePicker v-model="state.tanggal_lahir" class="form-input"></VueDatePicker>
            <small>*Masukkan tanggal lahir kamu</small>
          </div>
          <button class="btn-hitung" @click="hitung">{{ state.buttonText }}</button>
        </div>
        <result :tanggalLahir="state.sendResult" class="card-result" v-if="state.showResult" />
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, reactive } from 'vue';
import VueDatePicker from '@vuepic/vue-datepicker';
import result from '@/components/result.vue'
import '@vuepic/vue-datepicker/dist/main.css'

export default {
  name: 'app',
  components: {
    VueDatePicker,
    result,
  },
  setup() {
    const state = reactive({
      buttonText: 'Hitung',
      showResult: false,
      tanggal_lahir: null,
      sendResult: null,
    })

    function hitung() {
      state.buttonText = "Menghitung Umur Anda..."
      state.showResult = false
      setTimeout(() => {
        state.showResult = true
        state.buttonText = "Hitung"

        if (state.tanggal_lahir) {
          const birthDate = new Date(state.tanggal_lahir);
          const today = new Date();

          let years = today.getFullYear() - birthDate.getFullYear();
          let months = today.getMonth() - birthDate.getMonth();
          let days = today.getDate() - birthDate.getDate();

          if (months < 0) {
            years--;
            months += 12;
          }

          if (days < 0) {
            months--;
            const lastMonth = new Date(today.getFullYear(), today.getMonth(), 0);
            days += lastMonth.getDate();
          }

          state.sendResult = `${years} Tahun, ${months} Bulan, ${days} Hari `

        } else {
          console.log(null)
          state.sendResult = "Input dulu tanggal lahir anda..."
        }
      }, 1200);
    }

    onMounted(() => {
    })

    return {
      state,
      hitung,
    }
  }
}
</script>

<style scoped>
.container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.wrapper {
  /* border: 1px solid red; */
  width: 50%;
  height: 90vh;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.wrapper h2 {
  margin: 50px 0 20px 0;
  font-size: 30px;
}

.wrapper .card {
  /* border: 1px solid black; */
  background-color: var(--background-color);
  border-radius: 5px;
  width: 100%;
  height: 40%;
  display: flex;
  margin-bottom: 10px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.wrapper .card-result {
  /* border: 1px solid black; */
  background-color: var(--background-color);
  border-radius: 5px;
  width: 100%;
  height: 30%;
  display: flex;
  margin-bottom: 10px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.wrapper .card .form-group {
  /* border: 1px solid green; */
  width: 60%;
  height: fit-content;
  margin-bottom: 20px;
}

.wrapper .card .form-group .form-input {
  width: 90%;
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
  background-color: white;
  cursor: pointer;
  font-size: 1rem;
}

.wrapper .card .btn-hitung {
  border: none;
  background-color: var(--text-color);
  color: var(--background-color);
  padding: 7px 20px;
  border-radius: 11px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  transition: transform 0.6s, background-color 0.6s, color 0.6s, border 0.6s;
}

.wrapper .card .btn-hitung:hover {
  transform: scale(0.9);
  background-color: var(--background-color);
  color: var(--text-color);
  border: 1px solid var(--text-color);
}

.wrapper p {
  margin-top: 10px;
}

@media only screen and (max-width:700px) {
  .wrapper {
    width: 90%;
  }

  .wrapper h2 {
    font-size: 40px;
  }

  .wrapper .card .form-group {
    width: 90%;
  }

  .wrapper .card .form-group .form-input {
    width: 100%;
  }
}
</style>