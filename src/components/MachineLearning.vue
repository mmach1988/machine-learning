<template>
  <div> 
    <h1>{{title}}</h1>
    {{text}}
  </div>
</template>

<script>
import * as tf from "@tensorflow/tfjs"
import * as tfvis from "@tensorflow/tfjs-vis"
import { MnistData } from '../data.js';

export default {
  name: 'MachineLearning',
  props: {
    msg: String
  },
  data: () => ({
    title: 'tytuł',
    text: 'some text'
  }),
  methods: {
    init() {
      tf;
      tfvis;
      MnistData;

    }
  },
  created() {
    async function showExamples(data) {
    //create a container in the visor
    const surface = tfvis
    .visor()
    .surface({ name: "Imput Data Examples", tab: "Input Data" });
    // Get the examples
    const examples = data.nextTestBatch(20);
    const numExamples = examples.xs.shape[0];
    //Create a canvas element to redner each image
    for(let i=0; i<numExamples; i++) {
      const imageTensor = tf.tidy(() => {
            //Reshape the image to 28 x 28 px
            return examples.xs
            .slice([i,0], [examples.xs.shape[1]])
            .reshape([28, 28, 1]);
      });
      const canvas = document.createElement("canvas");
      canvas.width = 28;
      canvas.height = 28;
      canvas.style = "margin: 4px;";
      await tf.browser.toPixels(imageTensor, canvas);
      surface.drawArea.appendChild(canvas);

      imageTensor.dispose();
    }
  }
 //Run the process
    run();
    async function run() {
      const data = new MnistData();
      await data.load();
      await showExamples(data);
    }
  }
};

</script>

<style>

</style>
