<style>
.img-center {
    width: 200px;
    height: 150px;
    margin: 20px;
    overflow: hidden;
    position: relative;
}

.img-center img {
    display: block;
    position: absolute;
}

.img-center img.aspectFill-x {
    width: 100%;
    top: 50%;
    transform: translateY(-50%);
}

.img-center img.aspectFill-y {
    height: 100%;
    left: 50%;
    transform: translateX(-50%);
}
</style>

<script>
export default {
  methods: {
    imageLoad(img) {
      return new Promise(function(resolve, reject) {
        if (img.complete) {
          resolve()
        } else {
          img.onload = function(event) {
            resolve(event)
            }

          img.onerror = function(err) {
            reject(err)
          }
        }
      })
    },

      imageCenter(domList, mode) {
        domList.forEach(function(item) {
          var img = item.children[0]
          var itemW = item.offsetWidth
          var itemH = item.offsetHeight
          var itemR = itemW / itemH

          imageLoad(img).then(function() {
              var imgW = img.naturalWidth
              var imgH = img.naturalHeight
              var imgR = imgW / imgH

              var resultMode = null

              switch (mode) {
                  // 这样写是因为期待未来可以扩展其他的展示方式
                  case 'aspectFill':
                      resultMode = imgR > 1 ? 'aspectFill-x' : 'aspectFill-y'
                      break
                  case 'wspectFill':
                      resultMode = itemR > imgR ? 'aspectFill-x' : 'aspectFill-y'
                      break
                  default:
              }

              img.className += resultMode
            })
        })
    }
  }
}

</script>

<template>
  <section class="img-wrap">
    <div class="img-center">
      <img src="images/ewm.png"/>
    </div>

    <div class="img-center">
      <img src="images/project-index.png"/>
    </div>

    <div class="img-center">
      <img src="images/project-item.png"/>
    </div>

    <div class="img-center">
      <img src="images/project-score.png"/>
    </div>
  </section>
</template>
