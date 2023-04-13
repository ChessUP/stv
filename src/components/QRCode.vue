<template>
    <div ref="qrcode"></div>
  </template>
  
  <script>
  import QRCodeGenerator from "qrcode";
  
  export default {
    name: "QRCode",
    props: {
      value: {
        type: String,
        required: true,
      },
      options: {
        type: Object,
        default: () => ({}),
      },
    },
    mounted() {
      this.generateQRCode();
    },
    watch: {
      value() {
        this.generateQRCode();
      },
    },
    methods: {
      generateQRCode() {
        QRCodeGenerator.toCanvas(this.$refs.qrcode, this.value, this.options, (error) => {
          if (error) {
            console.error(error);
          }
        });
      },
    },
  };
  </script>
  