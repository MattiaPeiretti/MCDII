<template>
    <div>
        <p>{{data.name}}</p>
        <button @click="deleteCrumb">Delete</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            data: {},
        };
    },
    props: {
        data: {
        type: String,
        required: true,
        },
    },
    methods: {
    deleteCrumb(e) {
      this.$emit("deleteCrumb");
    }
  }
}
</script>