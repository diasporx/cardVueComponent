<template>
  <div class="container">
    <div class="bg-image">
      <div class="group-cards">
        <!-- card-front  -->
        <div class="card-front card">
          <div class="circles-group">
            <div class="circle-filled"></div>
            <div class="circle"></div>
          </div>
          <span class="number">{{ this.cardNumber !== '' ? this.cardNumber : '0000 0000 0000 0000' }}</span>
          <div class="group-card-text">
            <span class="name">{{ this.cardName !== '' ? this.cardName : 'Designed Credit' }}</span>
            <span class="exp_date">{{
                this.cardExpMonth !== '' ? this.cardExpMonth : '00'
              }} / {{ cardExpYear !== '' ? cardExpYear : '00' }}</span>
          </div>
        </div>
        <!-- card-front  -->

        <!-- card-back  -->
        <div class="card card-back">
          <span>{{ this.cardCvc !== '' ? this.cardCvc : '***' }}</span>
        </div>
        <!-- card-back  -->
      </div>
    </div>
    <div class="main">

      <!-- form  -->
      <div class="form">
        <div class="accept-form d-flex flex-column align-items-center justify-content-center"
             v-if="this.accept === true">
          <img src="../assets/images/icon-complete.svg" class="mb-2" alt="complete-svg">
          <h1>Thank you!</h1>
          <h4>We've added your card details</h4>
        </div>
        <div v-else>
          <span>Cardholder name</span>
          <div class="mb-1">
            <input @input="validationName(this.cardName)" class="w-100" :class="{err: this.errors.name !== ''}"
                   type="text" maxlength="22" placeholder="e.g. Jane Appleseed" v-model="cardName">
            <span class="error_msg" v-if="this.errors.name !== ''">{{ this.errors.name }}</span>
          </div>
          <span>Card number</span>
          <div class="mb-1">
            <input class="w-100" :class="{err: this.errors.number !== ''}" type="text"
                   placeholder="e.g. 1234 5678 9123 0000" v-model="cardNumber"
                   @input="formatCardNumber">
            <span class="error_msg" v-if="this.errors.number !== ''">{{ this.errors.number }}</span>
          </div>
          <div class="group-inputs mb-2">
            <div class="d-flex flex-column block-expDate">
              <span>exp. date (mm/yy)</span>
              <div class="d-flex form-exp-date">
                <input class="" :class="{err: this.errors.date !== ''}" type="text" placeholder="MM"
                       @input="formatCardExpMonth" v-model="cardExpMonth">
                <input class="" :class="{err: this.errors.date !== ''}" type="text" placeholder="YY"
                       @input="formatExpYear" v-model="cardExpYear">
              </div>
              <span class="error_msg" v-if="this.errors.date !== ''">{{ this.errors.date }}</span>
            </div>
            <div class="d-flex flex-column">
              <span>cvc</span>
              <input @input="formatCardCvc" :class="{err: this.errors.cvc !== ''}" placeholder="e.g. 123"
                     v-model="cardCvc" type="text" class="w-100">
              <span class="error_msg" v-if="this.errors.cvc !== ''">{{ this.errors.cvc }}</span>
            </div>
          </div>
          <button class="btn-confirm w-100" @click="this.validationForm()">Confirm</button>
        </div>
      </div>
      <!-- form  -->
    </div>
  </div>
</template>

<script>
import Functions from '@/components/__form/functions.vue';
import validate from "@/components/__form/validate.vue";

export default {
  name: 'Main',
  mixins: [Functions, validate],
  data() {
    return {
      accept: false,

      yearNow: new Date().getFullYear().toString().slice(-2),

      cardName: '',
      cardNumber: '',
      maskNumber: 'XXXX XXXX XXXX XXXX',
      cardExpMonth: '',
      cardExpYear: '',
      cardCvc: '',

      errors: {
        name: '',
        number: '',
        date: '',
        cvc: ''
      }
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
  @media screen and (max-width: 968px) {
    flex-direction: column;
    height: auto;
    justify-content: flex-start;
    min-height: min-content;
  }

  .bg-image {
    @media screen and (max-width: 1220px) {
      width: 100%;
    }
    @media screen and (max-width: 968px) {
      height: 200px;
      position: relative;
      align-items: baseline;
    }
    width: 33.3%;
    height: inherit;
    background: url(../assets/images/bg-main-desktop.png) no-repeat;
    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: center;

    .group-cards {
      position: absolute;
      z-index: 9;
      left: 150px;

      @media screen and (max-width: 1440px) {
        left: 100px
      }
      @media screen and (max-width: 1220px) {
        position: relative;
        left: 0;
      }
      @media screen and (max-width: 968px) {
        padding: 20px;
        display: flex;
        flex-direction: column-reverse;
        transform: scale(80%);
        top: -30px;
      }

      .card {
        width: 445px;
        position: relative;
        height: 245px;
        display: flex;
        border-radius: 15px;
        padding: 35px 25px;
        -webkit-box-shadow: 10px 11px 36px rgba(34, 60, 80, 0.43);
        -moz-box-shadow: 10px 11px 36px rgba(34, 60, 80, 0.43);
        box-shadow: 10px 11px 36px rgba(34, 60, 80, 0.43);
        @media screen and (max-width: 968px) {
          height: 200px;
          width: 350px;
        }
      }

      .card-front {
        @media screen and (max-width: 1440px) {
          left: 0;
        }
        @media screen and (max-width: 968px) {
          margin-top: -70px;
          z-index: 10;
          margin-left: -30px;
        }
        margin-bottom: 20px;
        background: url(../assets/images/bg-card-front.png) no-repeat;
        left: -25px;
        flex-direction: column;
        justify-content: end;
        text-transform: uppercase;


        .circles-group {
          position: absolute;
          padding: 30px;
          top: 0;
          left: 0;
          width: 100%;
          display: flex;
          align-items: center;
          justify-content: flex-start;
        }

        .circle-filled {
          background-color: #fff;
          border-radius: 50%;
          margin-right: 20px;
          width: 50px;
          height: 50px;
        }

        .circle {
          border: 1px solid #fff;
          border-radius: 50%;
          width: 25px;
          height: 25px;
        }
      }

      .card-back {
        @media screen and (max-width: 1440px) {
          left: 0;
        }
        @media screen and (max-width: 968px) {
          background-size: cover;
        }
        background: url(../assets/images/bg-card-back.png) no-repeat;
        left: 75px;
        flex-direction: column;
        justify-content: center;
        text-align: end;

        span {
          margin-right: 30px
        }
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
        @media screen and (max-width: 968px) {
          font-size: 19px;
          margin-bottom: 10px;
        }
      }
    }
  }

  .main {
    position: relative;
    height: inherit;
    width: 100%;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    @media screen and (max-width: 968px) {
      padding: 100px 0 0;
    }

    .form {
      max-width: 350px;
      display: flex;
      flex-direction: column;

      .accept-form {
        h1 {
          text-transform: uppercase;
          letter-spacing: .2rem;
        }
        h4 {
          color: #9f9f9f;
        }
      }

      .error_msg {
        letter-spacing: .07rem;
        font-size: 13px;
        margin-top: 3px;
        color: red;
      }

      .btn-confirm {
        background-color: rgb(34, 9, 48);
        color: #fff;
        padding: 10px 15px;
        border-radius: 7px;
        font-weight: 700;
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
        @media screen and (max-width: 386px) {
          flex-direction: column;
        }

        .block-expDate {
          margin-right: 10px;
          @media screen and (max-width: 386px) {
            margin-bottom: 10px;
          }
        }

        .form-exp-date {
          @media screen and (max-width: 386px) {
            justify-content: space-between;
          }

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
        font-weight: 500;
        font-size: 18px;
      }

      input.err {
        border: 2px solid red;
      }

      input:focus-visible {
        outline: none;
      }

      span {
        letter-spacing: .15rem;
        margin-bottom: 7px;
        font-size: 15px;
        font-weight: 700;
        text-transform: uppercase;
        color: #302835;
      }
    }
  }
}
</style>
