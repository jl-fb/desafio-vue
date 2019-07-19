<template>
  <div id="app">
    <Header></Header>
    <Form></Form>
  </div>
</template>

<script>
import Header from "./components/Header";
import Form from "./components/Form";

export default {
  name: "app",
  components: {
    Header,
    Form
  }
};
</script>

<style>
body {
  background: linear-gradient(
    to right,
    rgb(201, 201, 238),
    rgb(160, 160, 230),
    rgb(137, 137, 230),
    rgb(117, 117, 231)
  );
}
</style>
