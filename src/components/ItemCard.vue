<template>
  <div class="card p-3">

      <div class="card-body">
        <h4 class="card-title">{{ item.firstName }} </h4>
        <h5 class="card-title">{{ item.phone }} </h5>
        <h5 class="card-title">{{ item.email }} </h5>
        <h5 class="card-title">{{ item.address.city }} </h5>
      </div>
      <div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
    };
  },
  filters: {
  },
  props: {
    // this component expects a prop of type object
    item: {
      type: Object,
      required: true
    }
  }
};
</script>