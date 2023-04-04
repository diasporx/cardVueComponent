<template>
  <div class="container">
    <div class="bg-image"></div>
    <div class="main">

      <!-- card-front  -->
      <div class="card-front">
        <span class="number" v-if="this.cardNumber != ''">{{ this.cardNumber }}</span>
        <span class="number" v-else>XXXX XXXX XXXX XXXX</span>
        <div class="group-card-text">
          <span class="name" v-if="this.cardName != ''">{{ this.cardName }}</span>
          <span class="name" v-else>Alex Design</span>
        </div>
      </div>
      <!-- card-front  -->

      <!-- form  -->
      <div class="form">
        <span>Cardholder name</span>
        <input class="mb-1" type="text" v-model="cardName">
        <span>Card number</span>
        <input class="mb-1" type="text" v-model="cardNumber" @input="formatCardNumber">
      </div>
      <!-- form  -->
    </div>
  </div>
</template>

<script>

export default {
  name: 'Main',
  data() {
    return {
      cardName: '',
      cardNumber: '',
    }
  },
  methods: {
    formatCardNumber() {
      this.cardNumber = this.cardNumber.replace(/\D/g, '');
      if (this.cardNumber.length > 16) {
        this.cardNumber = this.cardNumber.slice(0, 16);
      }
      this.cardNumber = this.cardNumber.replace(/(\d{4})(?=\d)/g, '$1 ');
    }

  }
}
</script>

<style scoped lang="scss">
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

    .card-front {
      background: url(../assets/images/bg-card-front.png) no-repeat;
      width: 445px;
      position: absolute;
      height: 245px;
      left: -300px;
      border-radius: 15px;
      padding: 25px 25px;
      display: flex;
      flex-direction: column;
      justify-content: end;

      .group-card-text {
        display: flex;
        align-items: center;
        justify-content: space-between;

        span.name {
          color: #fff;
        }
      }

      span.number {
        color: #fff;
        font-size: 28px;
        margin-bottom: 15px;
      }
    }

    .form {
      min-width: 390px;
      display: flex;
      flex-direction: column;

      input {
        padding: 15px 20px;
        border-radius: 12px;
        width: 100%;
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
        letter-spacing: .35rem;
        margin-bottom: 7px;
        text-transform: uppercase;
        color: #302835;
      }
    }
  }
}
</style>
