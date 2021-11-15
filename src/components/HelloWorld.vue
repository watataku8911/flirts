<!-- eslint-disable -->
<template>
  <div class="hello">
    <div class="preview">
      <div class="loading">
        <pulse-loader :loading="loading"></pulse-loader>
      </div>
      <div class="imageBox" v-show="hide">
        <p v-if="rand == 0">
          <img src="@/assets/play.png" alt="やってる" style="max-width: 100%;">
        </p>
        <p v-else-if="rand == 1">
          <img src="@/assets/natural.png" alt="天然" style="max-width: 100%;">
        </p>
      </div>
      <div class="imagePreview">  
          <img :src="this.uploadedImage" alt="" class="image"/>
      </div>
    </div>
    <div class="buttons">
      <label for="corporation_file" class="btn btn-success">
        Select Image
        <input type="file" class="file_input" style="display:none;"
        id="corporation_file" mulitple="multiple"
        @change="onDrop">
      </label>
      <label class="btn btn-success" @click="click()">Diagnose</label>
    </div>
    <div class="errMsg">
      <p><font color="red" v-show="errMsgFlg">Selected Image.</font></p>
      <p><font color="red" v-show="errSelectingImageMsgFlg">Not Image.</font></p>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import PulseLoader from "vue-spinner/src/PulseLoader";

export default {
  name: 'HelloWorld',
  components: {
    PulseLoader
  },
  data () {
    return {
      rand: Math.floor(Math.random() * Math.floor(2)),
      hide: false,
      loading: false,
      flg: false,
      isDropingFlg: false,
      uploadedImage: "",
      errMsgFlg: false,
      errSelectingImageMsgFlg: false
    }
  },
  methods: {
        onDrop(event){
          this.errSelectingImageMsgFlg = false;
          this.hide = false;
          this.isDropingFlg = true;
          let fileList = event.target.files || e.dataTransfer.files;
          switch (fileList[0].type) {
            case "image/png":
              this.createImage(fileList[0]);
              break;
            case "image/jpg":
              this.createImage(fileList[0]);
              break;
            case "image/jpeg":
              this.createImage(fileList[0]);
              break;
            case "image/JPG":
              this.createImage(fileList[0]);
              break;
            case "image/gif":
              this.createImage(fileList[0]);
              break;
            default:
              this.errSelectingImageMsgFlg = true;
              break;
          }

        },
        // アップロードした画像を表示
        createImage(file) {
          let reader = new FileReader();
          reader.onload = (e) => {
              this.uploadedImage = e.target.result;
          };
          reader.readAsDataURL(file);
        },
        click() {
          if(this.isDropingFlg) {
            this.hide = false;
            this.errMsgFlg = false;
            this.loading = true; 
            setTimeout(()=>{
              this.loading = false;
              this.rand = Math.floor(Math.random() * Math.floor(2));
              //console.log(this.rand);
              this.hide = true;
              //console.log(this.hide);
            }, 2000)
          } else {
            //Not Dropping
            this.errMsgFlg = true;
          }
        },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*PC*/
@media screen and (min-width:1026px){
  .hello {
    margin-top: 50px;
  }

  .preview {
    margin-top: 2vh;
    width: 30%;
    height: 60vh;
    margin-left: auto;
    margin-right: auto;
    border: solid 2px black;
  }

  .loading {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translateY(-50%) translateX(-50%);
    -webkit-transform: translateY(-50%) translateX(-50%);
  }

  .imageBox {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translateY(-50%) translateX(-50%);
    -webkit-transform: translateY(-50%) translateX(-50%);
    transform: rotate(-10deg);
    -moz-transform: rotate(-10deg);
    -webkit-transform: rotate(-10deg);
  }

  

  .preview .image {
    width: 100%;
    height: 59vh;
  }

  .buttons {
    width: 80%;
    margin-top: 3vh;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    justify-content: space-between;
  }

  label {
    width: 20%;
    background-color: #cdebf7;
    text-align: center;
    padding: 1%;
    box-shadow:1px 1px 8px 0px #000;
  }

  .errMsg {
    text-align: center;
    font-size: 3vh;
  }
}

/*タブレット*/
@media screen and (min-width:482px) and (max-width:1025px){
  .hello {
    padding-bottom: 20vh;
    margin-top: 80px;
  }

  .preview {
    margin-top: 2vh;
    width: 80%;
    height: 65vh;
    margin-left: auto;
    margin-right: auto;
    border: solid 2px black;
  }

  .loading {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translateY(-50%) translateX(-50%);
    -webkit-transform: translateY(-50%) translateX(-50%);
  }

  .imageBox {
    position: absolute;
    top: 40%;
    left: 30%;
    transform: translateY(-50%) translateX(-50%);
    -webkit-transform: translateY(-50%) translateX(-50%);
    transform: rotate(-10deg);
    -moz-transform: rotate(-10deg);
    -webkit-transform: rotate(-10deg);
  }
    

  .preview .image {
    width: 100%;
    height: 65vh;
  }

  .buttons {
    width: 85%;
    margin-top: 5vh;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    justify-content: space-between;
  }

  label {
    width: 30%;
    background-color: #cdebf7;
    text-align: center;
    padding: 1%;
    box-shadow:1px 1px 8px 0px #000;
  }

  .errMsg {
    text-align: center;
    font-size: 3vh;
  }
}
/*スマホ*/
@media screen and (max-width:481px){

  .preview {
    margin-top: 2vh;
    width: 90%;
    height: 60vh;
    margin-left: auto;
    margin-right: auto;
    border: solid 2px black;
  }

  .loading {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translateY(-50%) translateX(-50%);
    -webkit-transform: translateY(-50%) translateX(-50%);
  }

  .imageBox {
    position: absolute;
    top: 30%;
    transform: translateY(-50%) translateX(-50%);
    -webkit-transform: translateY(-50%) translateX(-50%);
    transform: rotate(-45deg);
    -moz-transform: rotate(-45deg);
    -webkit-transform: rotate(-45deg);
  }
    

  .preview .image {
    width: 100%;
    height: 59.5vh;
  }

  .buttons {
    width: 90%;
    margin-top: 5vh;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    justify-content: space-between;
  }

  label {
    width: 35%;
    background-color: #cdebf7;
    text-align: center;
    padding: 1%;
    box-shadow:1px 1px 8px 0px #000;
  }

  .errMsg {
    margin-top: 1.5vh;
    text-align: center;
    font-size: 3vh;
  }
}


</style>
