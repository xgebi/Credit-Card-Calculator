<template>
  <div class="home">
    <section
      class="disclaimer"
    >Disclaimer: Author of this app is a developer with interest in finance, not a financial advisor. This app is only informatory and numbers might differ from your bank's calculations.</section>
    <section>
      <form>
        <div>
          <label for="cur-loan">Current loan:</label>
          <input type="number" id="cur-loan" v-model="curLoan" step="0.01" min="0" />
        </div>
        <div>
          <label for="min-payment">Regular payment:</label>
          <input type="number" id="reg-payment" v-model="regPayment" step="0.01" min="0" /> %
        </div>
        <div>
          <label for="int-rate">Interest rate:</label>
          <input type="number" id="int-rate" v-model="intRate" step="0.01" min="0" /> %
        </div>
        <div>
          <label for="lowest-payment">Lowest possible payment:</label>
          <input type="number" id="lowest-payment" v-model="lowestPayment" step="0.01" min="0" />
        </div>
        <button v-on:click="calculate">Calculate</button>
        <button v-on:click="clear">Clear</button>
      </form>
    </section>
    <section v-if="payments.length > 0">
      <table>
        <thead>
          <tr>
            <th>Payment number</th>
            <th>Payment amount</th>
            <th>Payment interest</th>
            <th>Remaining</th>
          </tr>
        </thead>
        <tr v-for="payment in payments" v-bind:key="payment.number">
          <td>{{ payment.number }}</td>
          <td>{{ payment.amount.toFixed(2) }}</td>
          <td>{{ payment.interest.toFixed(2) }}</td>
          <td>{{ payment.remaining.toFixed(2) }}</td>
        </tr>
      </table>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "home",
  components: {},
  data() {
    return {
      payments: [],
      curLoan: 0.0,
      regPayment: 0.0,
      intRate: 0.0,
      lowestPayment: 0.0
    };
  },
  methods: {
    calculate() {
      this.payments = [];
      let loan = this.curLoan;

      while (loan >= this.lowestPayment) {
        let payment = {
          number: this.payments.length,
          amount: (this.regPayment / 100) * loan,
          interest: ((loan / 12) * this.intRate) / 100
        };
        payment["remaining"] = loan - payment.amount;
        if (payment.amount + payment.interest < 100) {
          break;
        }
        this.payments.push(payment);
        loan = payment["remaining"];
      }
    },
    clear() {
      this.payments = [];
    }
  }
};
</script>
