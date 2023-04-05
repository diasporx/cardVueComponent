<script>
export default {
  methods: {
    // validationForm() {
    //   const pattern = /^[a-zA-Z]+\s[a-zA-Z]+$/;
    //   if(!pattern.test(this.cardName)) {
    //     return true
    //   }
    // },
    formatCardNumber() {
      this.cardNumber = this.formatField(this.cardNumber, 16);
    },

    formatCardCvc() {
      this.cardCvc = this.formatField(this.cardCvc, 3);
    },

    formatCardExpMonth() {
      this.cardExpMonth = this.cardExpMonth.replace(/\D/g, '');
      if (this.cardExpYear.length > 2) {
        this.cardExpMonth = this.cardExpMonth.slice(0, 2);
      }
      if (this.cardExpMonth > 12) {
        this.cardExpMonth = ''
      }
    },

    formatExpYear() {
      this.cardExpYear = this.removeNonDigits(this.cardExpYear)
      if (this.cardExpYear.length > 2) {
        this.cardExpYear = this.cardExpYear.slice(0, 2);
      }
    },

    formatField(field, maxLength) {
      field = this.removeNonDigits(field);
      field = this.limitFieldLength(field, maxLength);
      field = this.formatFieldWithSpaces(field, 4);
      return field;
    },

    removeNonDigits(field) {
      return field.replace(/\D/g, '');
    },

    limitFieldLength(field, maxLength) {
      if (field.length > maxLength) {
        field = field.slice(0, maxLength);
      }
      return field;
    },

    formatFieldWithSpaces(field, spaceEvery) {
      return field.replace(new RegExp(`(\\d{${spaceEvery}})(?=\\d)`, 'g'), '$1 ');
    }
  }
}
</script>