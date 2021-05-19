<template>
  <div class="financialstatus">
    <h1>{{ msg }}</h1>

    <p>{{ error }}</p>
    <ul>
      <li v-for="account in accounts" v-bind:key="account.id">
          {{ account.iban }} - {{ account.bez }} - Saldo {{ account.has_transaction_aggregate.aggregate.sum.amount}}
      </li>
    </ul>
    <TransactionList />
  </div>
</template>

<script>
import TransactionList from "../components/TransactionList"
import gql from 'graphql-tag';

export const GET_ACCOUNTS = gql`
  query getAccounts {
  accounts(order_by: {bez: asc}, where: {is_customer: {online_id: {_eq: "123456789012"}}}) {
      iban
      id
      bez
      has_transaction_aggregate {
        aggregate {
          sum {
            amount
          }
        }
      }
    }
  }`;

export default {
  components: {
    TransactionList
  },
  name: 'FinancialStatus',
  props: {
    msg: String
  },
  data() {
    return {
     accounts: [
      ],
      error: null
    }
  },
  apollo: {
    accounts: {
      // graphql query
      query: GET_ACCOUNTS,
      error(error) {
        this.error = JSON.stringify(error.message);
      }
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
</style>
