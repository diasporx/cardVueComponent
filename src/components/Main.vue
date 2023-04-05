<template>
  <div class="container">
    <div class="bg-image"></div>
    <div class="main">

      <div class="group-cards">
        <!-- card-front  -->
        <div class="card-front card mb-2">
          <span class="number">{{ this.cardNumber !== '' ? this.cardNumber : '0000 0000 0000 0000' }}</span>
          <div class="group-card-text">
            <span class="name">{{ this.cardName != '' ? this.cardName : 'Designed Credit' }}</span>
            <span class="exp_date">00/00</span>
          </div>
        </div>
        <!-- card-front  -->

        <!-- card-back  -->
        <div class="card card-back">
          <span>{{ this.cardCvc != '' ? this.cardCvc : '***' }}</span>
        </div>
        <!-- card-back  -->
      </div>

      <!-- form  -->
      <div class="form">
        <span>Cardholder name</span>
        <input class="mb-1 w-100" type="text" maxlength="22" placeholder="e.g. Jane Appleseed" v-model="cardName">
        <span>Card number</span>
        <input class="mb-1 w-100" type="text" placeholder="e.g. 1234 5678 9123 0000" v-model="cardNumber"
               @input="formatCardNumber">
        <div class="group-inputs mb-2">
          <div class="d-flex flex-column me-1">
            <span>exp. date (mm/yy)</span>
            <div class="d-flex form-exp-date">
              <input class="" type="text" placeholder="MM" @input="formatCardExpMonth" v-model="cardExpMonth">
              <input class="" type="text" placeholder="YY" @input="formatExpYear" v-model="cardExpYear">
            </div>
          </div>
          <div class="d-flex flex-column">
            <span>cvc</span>
            <input @input="formatCardCvc" placeholder="e.g. 123" v-model="cardCvc" type="text" class="w-100">
          </div>
        </div>
        <button class="btn-confirm" @click="this.validationForm()">Confirm</button>
      </div>
      <!-- form  -->
    </div>
  </div>
</template>

<script>
import Functions from './__form/functions.vue';

export default {
  name: 'Main',
  mixins: [Functions],
  data() {
    return {
      cardName: '',
      cardNumber: '',
      maskNumber: 'XXXX XXXX XXXX XXXX',
      cardExpMonth: '',
      cardExpYear: '',
      cardCvc: ''
    }
  }
}
</script>

<style scoped lang="scss">
button {
  border: 0;
  outline: 0;
  transition: all .3s ease;
}

input::placeholder {
  color: #bcbcbc;
}

.container {
  display: flex;
  min-height: 100vh;
  height: 100vh;
  align-items: center;
  justify-content: center;

  .bg-image {
    width: 33.3%;
    height: inherit;
    background: url(../assets/images/bg-main-desktop.png) no-repeat;
    background-size: cover;
  }

  .main {
    position: relative;
    height: inherit;
    width: 100%;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;

    .group-cards {
      position: absolute;
      left: -300px;

      .card {
        width: 445px;
        position: relative;
        height: 245px;
        display: flex;
        border-radius: 15px;
        padding: 35px 25px;
      }

      .card-front {
        background: url(../assets/images/bg-card-front.png) no-repeat;
        left: -25px;
        flex-direction: column;
        justify-content: end;
        text-transform: uppercase;
      }

      .card-back {
        background: url(../assets/images/bg-card-back.png) no-repeat;
        left: 75px;
        flex-direction: column;
        justify-content: center;
        text-align: end;
        span {margin-right: 30px}
      }

      .group-card-text {
        display: flex;
        align-items: center;
        justify-content: space-between;
        color: #fff;
        letter-spacing: .1rem;
      }

      span.number {
        color: #fff;
        letter-spacing: .25rem;
        font-size: 26px;
        margin-bottom: 25px;
      }
    }

    .form {
      max-width: 350px;
      display: flex;
      flex-direction: column;

      .btn-confirm {
        background-color: rgb(34, 9, 48);
        color: #fff;
        padding: 10px 15px;
        border-radius: 7px;
        font-weight: 700;
        font-family: 'Space';
        font-size: 18px;
        letter-spacing: .1rem;
        cursor: pointer;
      }

      .btn-confirm:hover {
        background-color: rgb(50, 12, 71);
      }

      .btn-confirm:active {
        transform: scale(95%);
      }

      .group-inputs {
        display: flex;

        .form-exp-date {
          input {
            max-width: 100px;
            margin-right: 10px;
          }

          input:last-child {
            margin-right: 0;
          }
        }
      }

      input {
        padding: 7px 15px;
        border-radius: 7px;
        border: 2px solid #878bbd;
        font-family: 'Space';
        font-weight: 500;
        font-size: 18px;
      }

      input:focus-visible {
        border-radius: none;
        outline: none;
      }

      span {
        letter-spacing: .25rem;
        margin-bottom: 7px;
        font-size: 12px;
        text-transform: uppercase;
        color: #302835;
      }
    }
  }
}
</style>
