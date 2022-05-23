<template>
    <div class="row no-gutters">
      <div class=" card-height border card1" align="left">
        
        <div  v-for="(section, index) in sections" :key="index" class="section">
        <!-- <span>{{section}}</span> -->
        <input type="text" v-model="section.value" class="sectionname" />
        <div @click="edit(index)" class="dots"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-three-dots-vertical" viewBox="0 0 16 16">
  <path d="M9.5 13a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zm0-5a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zm0-5a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0z"/>
</svg>
<span >
</span>
</div>

        </div>
        <button class="button" @click="click()"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-plus add" viewBox="0 0 18 18">
  <path d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"/>
</svg> Add section</button>
      </div>
      <div class=" card-height border card2" id="infinite" infinite-wrapper style=" overflow: auto;">
        <div class="timeline">
          <li v-for="(index,j) in list" :key="j" style="display: inline; overflow-y: hidden; font-size: 0.8em" class="px-3">{{index}}</li>
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
      list1: [[{ name: "Task 1", section: 0}, {name: 'Task 2', section: 0}] ,  [{ name: "Task 3", section: 1}] , []],
      list2: [],
      list: [],
      sections: [{value : 'Section 1'} , {value: 'Todo'} , {value: "Session"}]
    };
  },
  components: {
    draggable,
  },
  mounted() {
        this.list =  [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30];
        let element = document.querySelector('#infinite');
        console.log(element)
        element.addEventListener("scroll", this.handleScroll);
    },  
  methods: {
    edit(edit)
    {
      console.log(edit)
    },
    nameChange(i){
      console.log(i)
    },
    click()
    {
    this.sections.push({value : 'Untitled Section'})
    console.log(this.sections)
    this.list1.push([])
    },
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
  padding: 0px 16px 0;
  line-height: 20px;
  margin: 0;
  display: flex;
  align-items: center;  
 transform: translateX(50px);

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
.sectionname{
 border: none;
 outline: none;
 width: calc(100% - 80px);
  cursor:pointer;
  padding: 5px 5px;
border-radius: 5px;
 /* display: block; */
}

.sectionname:focus{
  border: 1px solid #e1e1e1;
  outline: 2px solid blue;
  cursor:text

}
.button
{
  padding: 5px 10px 5px;
  margin-top: 10px;
 transform: translateX(56px);
 background-color: white;
 border: none;
 border-radius: 5px;
 color: rgb(131, 131, 131);
  transition: all linear 0.2s;
 
}
.button:hover
{
  transition: all linear 0.2s;
background-color: #ededed;
color: rgb(0, 0, 0);
}
.button .add{
  width: 0;
  transform-origin: center center;
  font-weight: 800;
  transition: all ease 0.4s;


}
.button:hover .add 
{
width: 20px;
transform-origin: center;
  transition: all ease 0.4s;
}


.dots
{
  padding: 5px 8px;
  color: rgb(110, 110, 110);
  border-radius: 100px;
  cursor: pointer;
}

.dots:hover
{
  background-image: radial-gradient(#ededed , white) ;
  
  box-shadow: 0px 0px 2px #ededed;
  color: black;
}
</style>