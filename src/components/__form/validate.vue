<script>
export default {
  name: "validate",
  methods: {
    validationForm() {
      this.validationName(this.cardName)
      this.validationNumber(this.cardNumber)
      this.validationExpMonth(this.cardExpMonth, this.cardExpYear)
    },

    validationName(name) {
      const pattern = /^[a-zA-Z]+\s[a-zA-Z]+$/;
      if (pattern.test(this.cardName)) {
        this.errors.name = ''
        return true
      } else {
        this.errors.name = 'Write full name'
        return false
      }
    },

    validationNumber(number) {
      if (number.length === 19) {
        this.errors.number = ''
        return true
      } else {
        this.errors.number = 'Wrong card number'
        return true
      }
    },

    validationExpMonth(month, year) {
      if (month !== '' && year !== '') {
        this.errors.date = ''
        if (year < this.yearNow) {
          this.errors.date = 'Expiration date'
          return false
        } else {
          this.errors.date = ''
          return true
        }
      } else {
        this.errors.date = 'Enter the correct date'
        return false
      }
    }
  }
}
</script>