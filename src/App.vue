<template>
  <div id="app">
    <div class="bg-img"></div>
    <div class="search-tag">
      <div class="tagChoose-container">
        <div
          class="tag-choose"
          v-for="(tag, index) in tagNameToFilter"
          :key="index"
        >
          <span class="tag">{{ tag }}</span
          ><i class="fas fa-times" @click="deleteTag(tag)"></i>
        </div>
      </div>
      <div class="clear-container" @click="clear()">
        <span>clear</span>
      </div>
    </div>
    <div class="container-job">
      <Jobcard
        v-for="(item, index) in getArrayJson"
        :key="index"
        :job="item"
        @getTag="update"
      />
    </div>
  </div>
</template>

<script>
import * as dataJson from "../exo-ressources/data.json";
import Jobcard from "./components/Jobcard.vue";
export default {
  name: "App",
  components: {
    Jobcard,
  },

  data() {
    return {
      tagNameToFilter: [],
    };
  },

  computed: {
    getArrayJson() {
      var tab = [];
      for (let key in dataJson) {
        for (let key1 in dataJson[key]) {
          if (key1 == "logo") {
            dataJson[key][key1].logo = require(dataJson[key][key1]);
          }
          tab.push(dataJson[key][key1]);
        }
      }

      return tab;
    },
  },
  methods: {
    filterTag(tag) {
      var tabJobcard = Array.from(
        document.getElementsByClassName("jobcard-content")
      );
      let tabLanguages = null;
      let tabTools = null;
      tabJobcard.forEach((elt) => {
        console.log(elt.dataset.languages);
        if (elt.dataset.languages.search(",") > 0) {
          tabLanguages = elt.dataset.languages.split(",");
        } else {
          tabLanguages = [elt.dataset.languages];
        }
        if (elt.dataset.tools.search(",") > 0) {
          tabTools = elt.dataset.tools.split(",");
        } else {
          tabTools = [elt.dataset.tools];
        }

        if (
          elt.dataset.role != tag &&
          elt.dataset.level != tag &&
          !tabLanguages.includes(tag) &&
          !tabTools.includes(tag)
        ) {
          elt.classList.add("hide");
        } else if (elt.classList.contains("hide")) {
          elt.classList.remove("hide");
        }
      });
    },

    update(tag) {
      if(! this.tagNameToFilter.includes(tag))
      this.tagNameToFilter.push(tag);
      this.filterTag(tag);
    },

    deleteTag(tag) {
      this.tagNameToFilter.splice(this.tagNameToFilter.indexOf(tag), 1);
      this.tagNameToFilter.forEach(tag=>{
        this.filterTag(tag)
      })

    },

    clear(){
      this.tagNameToFilter.splice(0)
      var tabJobcard = Array.from(document.getElementsByClassName("jobcard-content")
      );
      tabJobcard.forEach(elt=>{
        if (elt.classList.contains("hide")) {
                  elt.classList.remove("hide");
                }

      })
    }
  },
};
</script>

<style scoped lang="scss">
.hide {
  display: none;
}
#app {
  margin: 0;
  padding: 20px;
  width: 100vw;
  height: fit-content;
  min-height: 100vh;
  background-color: rgb(225, 248, 250);

  .bg-img {
    background-image: url("./assets/bg-header-desktop.svg");
    background-repeat: no-repeat;
    position: absolute;
    top: 0;

    width: 100vw;
    height: 30vh;
    background-color: rgb(91, 166, 162);
  }
  .search-tag {
    position: absolute;
    top: 25vh;
    left: 16%;
    width: 68vw;
    height: 60px;
    background-color: white;
    z-index: 3;
    border-radius: 5px;
    display: flex;
    padding: 10px;
  }
  .tagChoose-container {
    width: 80%;
    height: 100%;
    padding: 5px;
    display: flex;
    align-items: center;

    .tag-choose {
      margin-right: 10px;
      .tag {
        display: inline-block;
        background-color: rgb(225, 248, 250);
        color: rgb(91, 166, 162);
        height: 100%;
        padding: 0.4em;
        font-size: 13px;
        font-weight: bold;
        // border: 2px solid;
      }
      i {
        color: white;
        padding: 7px;
        background-color: rgb(91, 166, 162);
      }
      i:hover {
        cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
          auto;
        background-color: black;
        color: rgba(255, 255, 255, 0.822);
      }
    }
  }
  .clear-container {
    width: 20%;
    padding: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    span {
      color: rgb(91, 166, 162);
      font-weight: bold;
      text-decoration: underline;
    }
    span:hover {
      cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
        auto;
    }
  }
  .container-job {
    margin-top: 40vh;
  }
}
</style>
