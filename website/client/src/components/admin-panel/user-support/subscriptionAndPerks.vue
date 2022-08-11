<template>
  <div class="accordion-group">
    <h3
      class="expand-toggle"
      :class="{'open': expand}"
      @click="expand = !expand"
    >
      Subscription, Monthly Perks
    </h3>
    <div v-if="expand">
      <div v-if="subscription.paymentMethod">
        Payment Method:
        <strong>{{ subscription.paymentMethod }}</strong>
      </div>
      <div v-if="subscription.planId">
        Payment Schedule ("basic-earned" is monthly):
        <strong>{{ subscription.planId }}</strong>
      </div>
      <div v-if="subscription.dateCreated">
        Creation Date:
        <strong>{{ dateFormat(subscription.dateCreated) }}</strong>
      </div>
      <div>
        Termination Date:
        <strong
          v-if="subscription.dateTerminated"
        >
          {{ dateFormat(subscription.dateTerminated) }}
        </strong>
        <strong v-else> None </strong>
      </div>
      <div>
        Consecutive Months:
        <strong>{{ subscription.consecutive.count }}</strong>
      </div>
      <div>
        Months Until Renewal:
        <strong>{{ subscription.consecutive.offset || 1}}</strong>
      </div>
      <div>
        Gem Cap:
        <strong>{{ subscription.consecutive.gemCapExtra + 25 }}</strong>
      </div>
      <div
        v-if="subscription.extraMonths > 0"
      >
        Additional Credit (applied upon cancellation):
        <strong>{{ subscription.extraMonths }}</strong>
      </div>
      <div
        v-if="subscription.mysteryItems.length > 0"
      >
        Mystery Items:
        <span
          v-for="(item, index) in subscription.mysteryItems"
          :key="index"
        >
          <strong v-if="index < subscription.mysteryItems.length - 1"> {{ item }}, </strong>
          <strong v-else> {{ item }} </strong>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  props: {
    subscription: {
      type: Object,
      required: true,
    },
  },
  data () {
    return {
      expand: false,
    };
  },
  methods: {
    dateFormat (date) {
      return moment(date).format('YYYY/MM/DD');
    },
  },
};
</script>
