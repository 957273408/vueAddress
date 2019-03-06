<template>
  <div>
    <header>
      <div>{{addressText}}</div>
      <div>
        <button>提交</button>
        <button>查询</button>
      </div>
    </header>
    <ul class="tabs">
      <li :class="{active:ressActive==1}" @click="ressActive=1">省</li>
      <li :class="{active:ressActive==2}" @click="ressActive=2">市</li>
      <li :class="{active:ressActive==3}" @click="ressActive=3">区</li>
    </ul>
    <section v-show="ressActive==1" class="words">
      <div
        v-for="item in addresslist"
        :key="item.value"
        @click="province(item,item.value)"
        :class="{active:item.value==provinceid}"
      >{{ item.text }}</div>
    </section>
    <section v-show="ressActive==2" class="words">
      <div
        v-for="item in citylist"
        :key="item.value"
        @click="city(item,item.value)"
        :class="{active:item.value==cityid}"
      >{{ item.text }}</div>
    </section>
    <section v-show="ressActive==3" class="words">
      <div
        v-for="item in arealist"
        :key="item.value"
        @click="area(item,item.value)"
        :class="{active:item.value==areaid}"
      >{{ item.text }}</div>
    </section>
  </div>
</template>

<script>
import { init_city_picker } from "./assets/data.city.js";
export default {
  data() {
    return {
      addressText: "",
      addresslist: [],
      citylist: [],
      arealist: [],
      ressActive: 1,
      provinceid: "",
      provincename: "",
      cityid: "",
      cityname: "",
      areaid: "",
      areaname: ""
    };
  },
  created() {
    this.addresslist = init_city_picker;
  },
  methods: {
    province(e, id) {
      console.log(e);

      this.provinceid = id;
      this.provincename = e.text;
      this.addressText = this.provincename + " ";
      this.citylist = this.addresslist.find(e => {
        return e.value == id;
      }).children;
      this.ressActive++;
    },
    city(e, id) {
      this.cityname = e.text;
      this.cityid = id;
      this.addressText = this.provincename + " " + this.cityname;
      this.ressActive++;
      this.arealist = e.children;
    },
    area(e, id) {
      this.areaname = e.text;
      this.areaid = id;
      this.addressText =
        this.provincename + " " + this.cityname + " " + this.areaname;
    }
  }
};
</script>

<style lang='less'>
* {
  padding: 0m 0;
}
header {
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 50px;
  div:first-child {
    font-size: 26px;
  }
}
.tabs {
  list-style: none;
  display: flex;
  justify-content: center;
  align-items: center;
  li {
    width: 60px;
    height: 50px;
    line-height: 50px;
    border-bottom: 2px solid transparent;
    text-align: center;
    &.active {
      color: blue;
      border-bottom-color: yellowgreen;
    }
  }
}
.words {
  div {
    line-height: 50px;
    padding: 0 50px;
    border-bottom: 1px solid #ccc;
    &.active {
      color: skyblue;
    }
  }
}
</style>
