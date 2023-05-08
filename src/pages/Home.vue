<template lang="pug">
.home
  canvas#live2dCvs.cvs
  //- live2d(
  //- 	:style="''"
  //- 	:size="350"
  //- 	:apiPath="'/src/assets'"
  //- 	:model="['greeter', 'haru_greeter_t03.model3']"
  //- )
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, nextTick } from "vue";

export default defineComponent({
  name: "Home",
  // components: { live2d },
  setup: () => {
    const sceneDom = ref(null);

    // const cubism2Model =
    //   "https://cdn.jsdelivr.net/gh/guansss/pixi-live2d-display/test/assets/shizuku/shizuku.model.json";
    const cubism4Model =
      "https://cdn.jsdelivr.net/gh/guansss/pixi-live2d-display/test/assets/haru/haru_greeter_t03.model3.json";


    const init = async () => {
      const live2d = PIXI.live2d;
      const app = new PIXI.Application({
        view: document.getElementById("live2dCvs"),
        autoStart: true,
        resizeTo: window,
        backgroundColor: 0x333333,
        transparent: true
      });

      const models = await Promise.all([
        // live2d.Live2DModel.from(cubism2Model),
        live2d.Live2DModel.from(cubism4Model),
      ]);

      models.forEach((model) => {
        app.stage.addChild(model);

        const scaleX = (innerWidth * 0.4) / model.width;
        const scaleY = (innerHeight * 0.8) / model.height;

        // fit the window
        model.scale.set(Math.min(scaleX, scaleY));

        model.y = innerHeight * 0.1;

        // draggable(model);
        // addFrame(model);
        // addHitAreaFrames(model);
      });

      const model2 = models[0];
      // const model4 = models[1];

      model2.x = (innerWidth - model2.width) / 2;
      // model4.x = model2.x + model2.width;

      // handle tapping

      model2.on("hit", (hitAreas) => {
        if (hitAreas.includes("body")) {
          model2.motion("tap_body");
        }

        if (hitAreas.includes("head")) {
          model2.expression();
        }
      });

      // model4.on("hit", (hitAreas) => {
      //   if (hitAreas.includes("Body")) {
      //     model4.motion("Tap");
      //   }

      //   if (hitAreas.includes("Head")) {
      //     model4.expression();
      //   }
      // });
    };
    // const loadModel =  () => {
    // 	console.log(window.Live2DCubismCore)
    //   // window.loadlive2d('live2dCvs', '/src/assets/greeter/haru_greeter_t03.model3.json')
    //   // console.log(`Live2D 模型 ${this.modelPath}，服装 ${this.modelTexturesId} 加载完成`)
    // }
    onMounted(async () => {
      await init();
    });
    return { sceneDom };
  },
});
</script>

<style scoped>
.cvs {
  height: 450px;
  width: 500px;
  position: fixed;
  right: 2.5vw;
  bottom: 2.5vh;
}
</style>
