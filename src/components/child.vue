<template>
  <div class="row">
    <div class="side_menu">
      <div
        class="inside_children"
        v-for="(parent, index) in sampleJson(parentList)"
        :key="index"
        @click="getActiveValue(index, parent.children)"
      >
        <label class="parent_label">{{ parent.name }}</label>
      </div>
    </div>
    <div class="side_menu" v-if="showChild">
      <div
        class="inside_children"
        v-for="(children, index) of this.childrenList"
        :key="index"
        @click="getChildrenList(index, children.children)"
      >
        <label class="parent_label">{{ children.name }}</label>
      </div>
    </div>
    <div
      class="side_menu"
      v-if="showGrantChild && this.grandchildrenList != undefined"
    >
      <div
        class="inside_children"
        v-for="(children, index) of this.displayChildrenList"
        :key="index"
        @click="getGrantChildrenList(children.children)"
      >
        <label class="parent_label">{{ children.name }}</label>
      </div>
    </div>
    <div
      class="side_menu"
      v-if="showRemainingChild && this.displayGrantChildrenList != undefined"
    >
      <div
        class="inside_children"
        v-for="(children, index) of this.displayGrantChildrenList"
        :key="index"
        @click="getGrantChildrenList(children.children)"
      >
        <label class="parent_label">{{ children.name }}</label>
      </div>
    </div>
  </div>
</template>
<script>
import {
  sampleJson,
} from '@/utils.js';
export default {
  name: "HelloWorld",
  data() {
    return {
      showChild: false,
      showGrantChild: false,
      showRemainingChild: false,
      childrenList: [],
      displayChildrenList: [],
    };
  },
  methods: {
     sampleJson: sampleJson,
    getActiveValue(index, childrenName) {
      this.childrenList = [];
      this.childrenName = childrenName;
      this.childrenName.map((item) => {
        this.childrenList.push(item);
        this.showChild = true;
      });
      
      this.displayChildrenList = [];
      this.showGrantChild = false;
      this.showRemainingChild = false;
    },
    getChildrenList(index, grandchildrenList) {
      
      this.displayChildrenList = [];
      this.grandchildrenList = grandchildrenList;
      if(this.grandchildrenList != undefined){
        console.log("index", grandchildrenList);
          this.grandchildrenList.map((item) => {
        this.displayChildrenList.push(item);
        this.showGrantChild = true;
      });
      }
      this.showRemainingChild = false
    },
    getGrantChildrenList(values) {
      
      this.displayGrantChildrenList = [];
      this.grandchildrenName = values;
      if(this.grandchildrenName != undefined){
        console.log("values", values);
         this.grandchildrenName.map((item) => {
        this.displayGrantChildrenList.push(item);
        this.showRemainingChild = true;
      });
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
