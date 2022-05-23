<template>
    <div class="row no-gutters">
      <div class="col-md-3 card-height border pt-5" align="left">
        <h5 v-for="(section, index) in sections" :key="index" class="border-bottom">{{section}}</h5>
        <button>Add section</button>
      </div>
      <div class="col-md-8 card-height border" id="infinite" infinite-wrapper style=" overflow: scroll;">
        <li v-for="index in list" :key="index" style="display: inline; overflow-y: hidden; font-size: 0.8em" class="px-3">{{index}}</li>
        <div>
           <draggable :list="list1" group="my-group" class="pt-3 pb-2 border-bottom" @add="addedLog" @remove="removedLog">
            <li v-for="element in list1" :key="element.name" class="border m-2 p-2" style="display: inline;">
              {{ element.name }}
            </li>
          </draggable>
          <draggable :list="list2" group="my-group" class="pt-2 pb-2" @add="addedLog" @remove="removedLog">
            <li v-for="element in list2" class="border m-2 p-2" :key="element.name" style="display: inline;">
              {{ element.name }}
            </li>
          </draggable>
        </div>
      </div>
    </div>
</template>
<script>
import draggable from "vuedraggable";
export default {
  name: "ViewTimeline",
  data() {
    return {
      list1: [{ name: "Drag Me!", section: 0}, {name: 'himi', section: 0}],
      list2: [{ name: "Drag Me Too!", section: 1}],
      list: [],
      sections: ['Section 1', 'Section 2', 'Section 3']
    };
  },
  components: {
    draggable,
  },
  mounted() {
        this.list =  [1,2,3,4,54,5,56,5,21,1,23,4,65,6,2,3,4,5,6,6,7,8,8,90,2,1,1,1,1,1,12,3];
        let element = document.querySelector('#infinite');
        console.log(element)
        element.addEventListener("scroll", this.handleScroll);
    },  
  methods: {
    handleScroll() {
            let e = document.querySelector('#infinite');
            if(e.scrollLeft + e.clientWidth >= e.scrollWidth)
            {
                this.list.push(this.list[this.list.length - 1]+1)
            }
        },
        addedLog(e) {
          e.item._underlying_vm_ = e.newIndex;
          console.log(this.list1)
          console.log(this.list2)
        },
        removedLog(e) {
          console.log(e)
        }
  }
};
</script>
<style scoped>
.card-height {
  height: 500px;
}
</style>