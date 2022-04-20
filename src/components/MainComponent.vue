<template>
  <b-container class="main">
    <b-row cols="2">
      <b-col
          v-for="(item, index) in data" :key="item.id"
          class="p-4"
          :class="{ 'item-top': (index + 1) % 2 === 0 }"
      >
        <div class="mx-auto position-relative">
          <div>
            <b-icon icon="emoji-smile" font-scale="2" />
          </div>
          <div class="date p-2">
            {{ getCorrectDate(item.registered) }}
          </div>
          <div class="about mx-auto">
            {{ getSmallText(item.about) }}
          </div>
          <div
              class="item-line position-absolute"
              :class="(index + 1) % 2 === 0 ? 'left-line' : 'right-line'"
          >
            <span class="item-line-circle circle"></span>
            <span class="item-line-circle circle circle-white"></span>
            <div
                class="item-line-vertical position-absolute"
                :class="(index + 1) % 2 === 0 ? 'right-line-vertical' : 'left-line-vertical ' +
                (index === data.length-1 ? 'last-item-line-vertical' : '')"
            >
              <span class="item-line-vertical-circle"></span>
            </div>
          </div>
        </div>
      </b-col>
    </b-row>
  </b-container>
</template>
<script>
import informations from "../../informations.json"
import moment from "moment"

export default {
  name: 'MainComponent',

  data() {
    return {
      data: null
    }
  },
  mounted() {
    this.generateData();
  },
  methods: {
    generateData() {
      return this.data = informations.sort((a, b) => moment(a.registered) - moment(b.registered))
    },
    getCorrectDate(date) {
      return moment(date).format("MMM DD YYYY")
    },
    getSmallText(text) {
      return text.slice(0, 50)
    }
  }
}
</script>
<style>
  .date {
    color: #0b5184;
    font-weight: bold;
  }

  .about {
    max-width: 230px;
  }

  .item-line {
    top: 50%;
    width: 64px;
    background: #0b5184;
    height: 4px;
  }

  .item-line-vertical {
    top: 50%;
    width: 120px;
    background: #0b5184;
    transform: rotate(90deg);
    height: 4px;
  }

  .last-item-line-vertical {
    width: 180px !important;
    top: -18px !important;
    left: -28px !important;
  }

  .item-top {
    margin-top: 50px !important;
  }

  .left-line {
    left: -26px;
  }

  .right-line {
    right: -26px;
  }

  .left-line .item-line-circle {
    right: -3px;
  }

  .right-line .item-line-circle {
    left: -3px;
  }

  .left-line-vertical {
    left: 2px;
    top: -50px;
  }

  .circle {
    display: block;
    width: 15px;
    height: 15px;
    background: #0b5184;
    border-radius: 50%;
    position: absolute;
    top: -6px;
  }

  .left-line .circle-white {
    left: -5px !important;
  }

  .circle-white {
    left: 54px !important;
    background: #fff !important;
    z-index: 2;
    border: 3px solid #0b5184;
  }

  .circle-vertical {
    background: red !important;
  }

  .right-line-vertical {
    right: 2px;
  }
</style>
