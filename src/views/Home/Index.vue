<template>
  <div id="test">
    <input type="text" name="" v-model="url" id="">
    <button @click="convert">
      Convert
    </button>
  </div>
</template>

<script>

import { jsPDF } from 'jspdf';

export default {
  /**
   * The name of the page.
   */
  name: 'HomeIndex',
  data() {
    return {
      url: '',
    };
  },

  /**
   * The components that the page can use.
   */
  methods: {
    async convert() {
      // eslint-disable-next-line new-cap
      const doc = new jsPDF();

      fetch(this.url)
        .then((res) => res.text())
        .then((text) => {
          doc.html(text, {
            callback(docs) {
              docs.save();
            },
            x: 10,
            y: 10,
          });
        })
        .catch((err) => {
          console.log(err)
          alert(err)
        });
    },
  },
};
</script>
