<script setup>
  const props = defineProps(['memo', 'amount', 'date']);

  /**
   * 
   * @param {number} value 
   * @param {boolean} includeChange 
   */
  function toUSD(value, includeChange) {
    const opts = {};
    if (includeChange) {
      opts.minimumFractionDigits = 2;
      opts.maximumFractionDigits = 2;
    }

    return `\$${(value || 0).toLocaleString('en-US', opts)}`
  }
  /**
   * 
   * @param {Date} value 
   */
  function toDateString(value) {
    return new Date(value).toLocaleDateString('en-US', {
      month: 'short',
      day: '2-digit',
      year: 'numeric'
    });
  }
</script>

<template>
  <div :class="['record', (props.amount > 0) ? 'add' : 'pay']">
    <div class="memo">{{ props.memo }}</div>
    <div class="amount">{{ toUSD(props.amount) }}</div>
    <div class="date">{{ toDateString(props.date) }}</div>
  </div>
</template>

<style>
  .record {
    display: grid;
    grid-template-columns: 1fr max-content;
    font-size: 2em;
    padding: 1em;
    gap: 0.25em;
    border-bottom: 1px solid rgba(0, 0, 0, 0.25);
  }

  .record .memo {
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }
  .record .amount {
    font-size: 1.5em;
    font-weight: 300;
    align-self: center;
    grid-column: 2;
    grid-row: 1 / span 2;
  }
  .record .date {
    opacity: 0.5;
  }

  .record.add .amount {
    color: var(--color-danger);
  }
  .record.pay .amount {
    color: var(--color-primary);
  }
</style>