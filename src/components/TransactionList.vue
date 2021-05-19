<template>
    <div>
        <TransactionItem v-bind:transactions="transactions" />
    </div>
</template>

<script>
import gql from 'graphql-tag';
import TransactionItem from './TransactionItem.vue';

export const GET_TRANSACTIONS = gql`
    query getTransactions {
    transactions(where: {account_id: {_eq: "d821cde4-2f8d-45cf-9f57-01383e4d5b33"}}, order_by: {created_at: desc}) {
        id
        amount
        description
        created_at
    }
}`;

export default {
  components: {
    TransactionItem
  },
  data() {
    return {
      transactions: [
      ],
      error: null
    }
  },
  apollo: {
    transactions: {
      // graphql query
      query: GET_TRANSACTIONS,
      error(error) {
        this.error = JSON.stringify(error.message);
      }
    },
  },
}
</script>
