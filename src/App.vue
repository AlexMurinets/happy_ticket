<template>
  <v-app>
    <v-card
      class="mx-auto my-12"
        elevation="8"
        max-width="374">
    <div style="display:flex; justify-content:center; margin:20px">
    <h1>Счастливый билет</h1>
    </div>
    <div style="display:flex; justify-content:center; margin:20px; font-family: 'Raleway', sans-serif;">
<img src="https://kabacademy.eu/content/uploads/sites/5/2017/07/ticket1.png" alt="" width="300px" height="300px">
    </div>


<h2 align = "center">Номер билета</h2>
<v-form v-model="valid">
    <v-container>
          <v-text-field
            v-model="number"
            :rules="nameRules"
            :counter="6"
            label="Номер билета"
            required
          ></v-text-field>
    </v-container>
  </v-form>


      <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <div style="display:flex; justify-content:center; margin:20px">
         <v-btn
          :disabled="!valid"
          large
          rounded
          @click="openDialog()"
          color="warning"
          align="center"
          v-bind="attrs"
          v-on="on"
        >
          Проверить
        </v-btn>
        </div>
      </template>

      <v-card>
        <v-card-title :class= color>
          <div style="display:flex; justify-content:center; font-size:30px; color: white">
          {{message}}
          </div>
        </v-card-title>

        <v-card-text>
          <div style="display:flex; justify-content:center; font-size:20px; padding:20px">
          {{message1}}
          </div>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            Хорошо
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
      </v-card>
  </v-app>

</template>


<script>
export default {
  name: 'App',

 data: () => ({
      nextHappy: 0,
      count: 0,
      color: "primary",
      dialog: false,
      valid: false,
      number: '',
      message: 'Билет не счастливый.',
      message1: 'Ура вы счастливчик! Сьешьте его или сохраните в свою коллекцию счастливых билетиков!',
      nameRules: [
        v => !!v || 'Номер необходим',
        v => v.length == 6 || 'Должно быть 6 цифр',
      ],
    
    }),
   methods: {
    extractNumberFromPosition() {
    return((Math.floor(this.number/100000) + Math.floor(this.number/10000%10) + Math.floor(this.number/1000%10)) == (Math.floor(this.number/100%10) + Math.floor(this.number/10%10) + Math.floor(this.number%10)));
  },

  openDialog(){
      this.color = "primary"
      this.message = "Билет не счастливый!"
      
      if (this.extractNumberFromPosition() == true) {
        this.message = "Билет счастливый!"
        this.color = "success"
        this.message1 = "Ура вы счастливчик! Сьешьте его или сохраните в свою коллекцию счастливых билетиков!"
      }
      else{
      this.checkNumber()
      this.message1 = "Следующий счастливый билет будет через "+this.count+ ". Он равен " +this.nextHappy+". Повезет в следующий раз!"
      }
  },

    checkNumber() {
    this.count = 0
    for(let i = this.number; i<999999; i++)
    if((Math.floor(i/100000) + Math.floor(i/10000%10) + Math.floor(i/1000%10)) == (Math.floor(i/100%10) + Math.floor(i/10%10) + Math.floor(i%10))){
      this.nextHappy = i
      break
    }
    else this.count++
  },

}
}
</script>

<style scoped>
/* @import url(https://fonts.googleapis.com/css?family=Montserrat);

*{
  padding: 0;
  margin: 0;
  font-family: 'Montserrat';font-size: 22px;
  font-weight: 600;
} */
</style>
