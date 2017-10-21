<template>
    <div class="grid-padding">
        <grid-layout
            :layout="todos"
            :col-num="4"
            :row-height="100"
            :is-draggable="true"
            :is-resizable="true"
            :vertical-compact="true"
            :margin="[10, 10]"
            :use-css-transforms="true">
              <grid-item class="element-padding" v-for="item in todos" :key="item.i"
                   :x="item.x"
                   :y="item.y"
                   :w="item.w"
                   :h="item.h"
                   :i="item.i"
                   :id="item.i">
                   <p>{{item.title}}</p>
                   <p>
                       {{item.description}}
                   </p>
                   <div @click="onStatusToggle(item.i)" v-bind:class="{ active: item.completed }" class="toggle-btn ui bottom toggle attatched button">
                       {{ item.completed ? 'Completed' : 'Pending' }}
                   </div>
              </grid-item>
      </grid-layout>
    </div>
</template>

<script>
    import swal from 'sweetalert'
    import VueGridLayout from 'vue-grid-layout'
    import Firebase from 'firebase'

    let config = {
        apiKey: "AIzaSyATDg6rPfyO68BML0lS1jcu6PHwQ5eLvtc",
        authDomain: "mindo-project.firebaseapp.com",
        databaseURL: "https://mindo-project.firebaseio.com",
        projectId: "mindo-project",
        storageBucket: "mindo-project.appspot.com",
        messagingSenderId: "924031709286"
    }

    let app = Firebase.initializeApp(config);
    let db = app.database();
    let todosRef = db.ref('todo');

    var GridLayout = VueGridLayout.GridLayout;
	  var GridItem = VueGridLayout.GridItem;
    var columnNum = 4;
    export default {
        methods: {
            addGridElement(){
                var index = this.todos.length;
                var newGridElement = new gridElement("title", "info", index);
                this.todos.push(newGridElement)
            },
            onStatusToggle(index){
                this.todos[index].completed = !this.todos[index].completed
            }
        },
        firebase: {
          todos: todosRef
        },
        components: {
	        GridLayout,
	        GridItem,
	    },
    }

    class gridElement {
        constructor(title, description, index) {
            this.title = title;
            this.description = description;
            this.completed = false;
            this.i = index;
            this.x = this.i%columnNum;
            this.y = Math.floor(this.i/columnNum);
            this.w = 1;
            this.h = 1;
        }
    }
</script>

<style scoped>
.grid-padding {
    padding: 20px;
}

.element-padding {
    box-sizing: border-box;
    background-color: rgba(99, 213, 255, 1.0);
    box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.40);
}

.toggle-btn {
    border-radius: 0px !important;
    position: absolute !important;
    text-align: center !important;
    bottom: 0 !important;
    left: 0 !important;
    width: 100%;
}
</style>
