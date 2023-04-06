<script>
export default {
  name: "validate",
  methods: {
    validationForm() {
      const nameIsValid = this.validationName(this.cardName);
      const numberIsValid = this.validationNumber(this.cardNumber);
      const expMonthIsValid = this.validationExpMonth(this.cardExpMonth, this.cardExpYear);
      const cvcIsValid = this.validationCvc(this.cardCvc);

      if (nameIsValid && numberIsValid && expMonthIsValid && cvcIsValid) {
        this.accept = true
      }
    },

    validationName(name) {
      const pattern = /^[a-zA-Z]+\s[a-zA-Z]+$/;
      this.errors.name = pattern.test(name) ? '' : 'Write full name';
      return pattern.test(name);
    },
    validationNumber(number) {
      this.errors.number = number.length === 19 ? '' : 'Wrong card number';
      return number.length === 19;
    },
    validationExpMonth(month, year) {
      if (month !== '' && year !== '') {
        this.errors.date = '';
        const isExpired = year < this.yearNow;
        this.errors.date = isExpired ? 'Expiration date' : '';
        return !isExpired;
      } else {
        this.errors.date = 'Enter the correct date';
        return false;
      }
    },
    validationCvc(cvc) {
      this.errors.cvc = cvc.length < 3 ? 'CVC incorrect' : '';
      return cvc.length >= 3;
    }
  }
}
</script>
