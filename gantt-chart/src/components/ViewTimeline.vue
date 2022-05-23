<template>
    <div class="row no-gutters">
      <div class=" card-height border card1" align="left">
        
        <div  v-for="(section, index) in sections" :key="index" class="section">
        <span>{{section}}</span>
        </div>
        <button>Add section</button>
      </div>
      <div class=" card-height border card2" id="infinite" infinite-wrapper style=" overflow: auto;">
        <div class="timeline">
          <li v-for="index in list" :key="index" style="display: inline; overflow-y: hidden; font-size: 0.8em" class="px-3">{{index}}</li>
        </div>
        
        <div v-for="(list, index) in list1" :key="index" class="dragboard">
           <draggable :list="list" group="my-group" class="dragline" @add="addedLog" @remove="removedLog" style="min-height: 50px">
            <li v-for="element in list" :key="element.name"  style="display: inline;" class="dragli">
              
           
              <span class="element">{{ element.name }}</span>
               <!-- <span class="drag" >
                 <span class="element ">{{ element.name }}</span>
            </span> -->
            </li>
          </draggable>
          <div class="fix">
            <div class="borderb"></div>

          </div>
          <!-- <draggable :list="list2" group="my-group" class="dragline" @add="addedLog" @remove="removedLog" style="min-height: 50px">
            <li v-for="element in list2" class="border m-2 p-2 element" :key="element.name" style="display: inline;">
              {{ element.name }}
            </li>
          </draggable> -->
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
      list1: [[{ name: "Drag Me!", section: 0}, {name: 'himi', section: 0}] ,  [{ name: "Drag Me Too!", section: 1}] , []],
      list2: [],
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
  /* margin: 80px 0 0 0; */
}

.card1
{
  padding: 50px 0 0 10px;
  border-top: 1px solid black;
  width: 25%;

}
.card1::before{
 content: "";
    display: block;
    position: fixed;
    width:calc(25%);
    background-color: #e1e1e1;
    height: 2.5px;

}

.card2
{
  padding: 0;
  width: calc(75% - 50px);
}
.timeline
{
  
  margin: 26px 0 0 0;
  text-align: left;
}
.timeline::after{
 content: "";
    display: block;
    position: fixed;
    width:calc(75% - 33px);
    background-color: #e1e1e1;
    height: 2.5px;
    z-index: 0;

}
.section
{
  min-height: 50.5px;
  height: 50px;
  padding: 5px 16px 0;
  line-height: 20px;
  margin: 0;
  display: flex;
  align-items: center;
}

.dragline
{
  min-height: 50px;
  height: 50px;
  line-height: 49px;
  position: relative;
  padding-top: 2.5px;

}

.element
{
  z-index: 5;
border: 1px solid #e1e1e1;
padding: 7px 20px;
margin: 0 5px;
border-radius: 4px;
background-color: white;
}

.element:hover{
  border: 2px solid blue;
  border-right: 10px solid blue;
  border-left: 10px solid blue;
  padding: 7px 11px;
}
/* .dragli{
  position: relative;
}
.dragli .drag{
 display: none;
  position: absolute;
  height: 40px;
  width: calc(100% + 10px);
  background: blue;
  
  left: 0;
  z-index: 1;}
.dragli:hover .drag{
display: inline;
}
.drag .element
{
  margin: -5px  0 0;
} */
.element
{
cursor: grab;
}

.element:active{
  cursor:grabbing
}

.dragboard
{
  position: relative;
}
.dragboard .fix{
position: fixed;
padding: 0 0 -2px;
}
.fix .borderb
{
position: fixed;
border-bottom: 1px solid #e1e1e1;

width: calc(100% - 38px);
left: 0;
}
</style>