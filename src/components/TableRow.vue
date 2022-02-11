<template>
  <tr>
    <td>{{ description }}</td>
    <td>{{ value }}</td>
  </tr>
</template>
<script>
export default {
  name: "TableRow",
  props: {
    description: String,
    value: String,
  },
  data() {
    return {};
  },
  mounted() {},
};
</script>
