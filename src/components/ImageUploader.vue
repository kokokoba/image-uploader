<template>
  <div id="image-uploader">
    <div class="image-uploader-container">
      <h1 class="title">Upload user Image</h1>
      <span class="sub-title">File should be Jpeg, Png...</span>
      <div class="image-uploader-input">
        <div class="image-uploader-input-field"
        :class="{ over: isDragOver }"
         @dragover.prevent="onDrag('over')"
         @dragleave="onDrag('leave')"
         @drop.stop="onDrop"
        >
          <img src="../assets/image.svg">
          <span>Drag & Drop your image here</span>
        </div>
        <label class="image-uploader-label">
          Choose a file
          <input type="file" name="upload-file" @change="onChange" accept="image/*"/>
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageUploader',
  data() {
    return {
      isDragOver: false,
      image: null
    }
  },
  methods: {
    onDrag(type) {
      this.isDragOver = type === 'over'

    },
    onDrop(event) {
      this.isDragOver = false
      const files = event.dataTransfer.files
      if(files.length !== 1 || files[0].type.indexOf("image") !== 0) {
        return
      }
      this.readImage(files[0])

    },
    onChange(event) {
      const files = event.target.files
      if(files.length !== 1 || files[0].type.indexOf("image") !== 0) {
        return
      }
      this.readImage(files[0])
    },
    readImage(file) {
      const reader = new FileReader()
      reader.onload = this.loadImage
      reader.readAsDataURL(file)

    },
    loadImage(e) {
      let image = new Image()
      image.src = e.target.result
      this.image = image
    }
  }
}
</script>

<style scoped>
#image-uploader {
  position: absolute;
  width: 402px;
  height: 469px;
  left: 520px;
  top: 304px;
  background: #FFFFFF;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border-radius: 12px;
}

.image-uploader-container {
  padding: 36px 32px;
}

.title {
  height: 27px;
  font-family: Poppins;
  font-style: normal;
  font-size: 18px;
  line-height: 27px;
  letter-spacing: -0.035em;
  color: #4F4F4F;
}

.sub-title {
  height: 15px;
  font-family: Poppins;
  font-style: normal;
  font-size: 10px;
  line-height: 55px;
  text-align: center;
  letter-spacing: -0.035em;
  color: #828282;
}

.image-uploader-input-field {
  width: 338px;
  height: 219px;
  background: #F6F8FB;
  border: 2px dashed #97BEF4;
  box-sizing: border-box;
  border-radius: 12px;
}
.image-uploader-input-field:hover {
  opacity: 0.9;
  transition: 0.5s;
}

.image-uploader-input-field .over {
  background-color: #666;
}
.image-uploader-input-field img {
  display: block;
  margin: 35px auto 0;
}

.image-uploader-input-field span {
  display: block;
  margin: 37px auto 0;
  width: 166px;
  font-family: Poppins;
  font-style: normal;
  font-weight: 500;
  font-size: 12px;
  line-height: 18px;
  letter-spacing: -0.035em;
  color: #BDBDBD;
}

.image-uploader-label {
  display: inline-block;
  margin-top: 54px;
  padding: 8px 16px;
  color: #FFF;
  transition: 0.2s;
  cursor: pointer;
  background: #2F80ED;
  border-radius: 1.5em;
  font-family: Noto Sans;
  letter-spacing: -0.035em;
}

.image-uploader-label:hover {
  box-shadow: 0 8px 10px -2px rgba(0, 0, 0, 0.2);
}
.image-uploader-label input {
  display: none;
}
</style>
