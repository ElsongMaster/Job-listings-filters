<template>
  <div
    :class="
      job.featured ? 'jobcard-content border-featured' : 'jobcard-content'
    "
    :data-role="job.role"
    :data-level="job.level"
    :data-languages="job.languages"
    :data-tools="job.tools"
  >
    <div class="img-content">
      <img :src="require('@/assets/' + job.logo)" alt="" />
    </div>
    <div class="details-job">
      <p class="header-details">
        <span class="company">{{ job.company }}</span>
        <span v-if="job.new" class="new">New !</span>
        <span v-if="job.featured" class="featured"> Featured</span>
      </p>
      <a href="" class="position">{{ job.position }}</a>
      <div class="time-content">
        <span class="postedAt">{{ job.postedAt }}</span>
        <ul class="list">
          <li>{{ job.contract }}</li>
          <li>{{ job.location }}</li>
        </ul>
      </div>
    </div>
    <div class="tag-job">
      <p class="tag-content">
        <span class="tag" @click="sendTagChoose(job.role)">{{ job.role }}</span
        ><span class="tag" @click="sendTagChoose(job.level)">{{ job.level }}</span>
        <span
          class="tag"
          v-for="(language, index) in job.languages"
          :key="index"
           @click="sendTagChoose(language)">{{ language }}</span
        >
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Jobcard",
  props: {
    job: Object,
  },

  methods: {
    sendTagChoose(tag) {
    //   console.log(tag);
      this.$emit('getTag', tag);
      // this.$emit('update-cart', item)
    },
  },
};
</script>

<style scoped lang="scss">
.jobcard-content {
  height: 125px;
  width: 70%;
  background-color: white;
  margin: 30px auto;
  border-radius: 10px;
  display: flex;
  padding: 5px;
  box-shadow: 5px 5px 5px 5px rgba(0, 0, 0, 0.2);
  transition: 0.2s ease-in-out;

  .img-content {
    width: 15%;
    height: 100%;
    display: flex;
    justify-content: center;
    padding: 10px;
  }
  .details-job {
    padding: 5px;
    // border:2px solid;
    width: 40%;

    .header-details {
      margin: 10px 0;

      .company,
      .new,
      .featured {
        font-size: 13px;
        font-weight: bold;
        color: white;
      }
      .company {
        color: rgb(94, 168, 167);
      }
      .new,
      .featured {
        text-transform: uppercase;
        padding: 5px;
        border-radius: 40%;
      }
      .new {
        background-color: rgb(94, 168, 167);
      }
      .featured {
        background-color: black;
      }
    }
  }
  .position {
    color: rgb(41, 50, 49);
    font-weight: bold;
  }
  .position:hover {
    cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
      auto;
    color: rgb(94, 168, 167);
  }
  .time-content {
    display: flex;
    justify-content: space-between;
    margin-top: 5px;
    // border: 2px solid;
    padding-left: 0;
    width: 75%;

    * {
      color: rgb(151, 157, 157);
      font-size: 13px;
    }
    .postedAt {
      text-align: left;
      // border: 2px solid;
      width: 20%;
    }
    .list {
      display: flex;
      justify-content: space-between;
      width: 65%;
      list-style-type: disc;
    }
  }
  .tag-job {
    width: 50%;
    display: flex;
    align-items: center;

    .tag-content {
      width: 100%;
      display: flex;
      justify-content: space-between;

      .tag {
        text-align: center;
        padding: 5px;
        background-color: rgb(225, 248, 250);
        color: rgb(94, 168, 167);
        font-weight: bold;
      }
      .tag:hover {
        cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
          auto;

        background-color: rgb(94, 168, 167);

        color: white;
      }
    }
  }
}
.jobcard-content:hover {
  transform: translateY(10px);
}
.border-featured {
  border-left: 5px solid rgb(94, 168, 167) !important;
}
</style>
