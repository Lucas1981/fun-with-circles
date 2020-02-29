<template>
  <div>
    <div class="input-group input-group-sm mb-3">
      <div class="input-group-prepend">
        <span class="input-group-text" id="inputGroup-sizing-sm">{{ label }}</span>
      </div>
      <input
        :value="value"
        :type="type"
        class="form-control"
        @change="$emit('input', $event.target.value)"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'label',
    'type',
    'value'
  ]
};
</script>
