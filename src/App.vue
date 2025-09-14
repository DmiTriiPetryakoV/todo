<template>

    <p>ToDo-List</p>
    <div id="BoxApp">
      <div id="section">
      <input id="UserTasks" placeholder="Сюда задачу" maxlength="35" v-model="newTasks"/>
      <button id="AddTasks" @click="AddTasks">Добавить задачу</button>
      </div>
      <div id="BoxApp2" >
       
      <div v-for="(task, index) in tasks" :key="task.id" :id="`task-${task.id}`" class="rowList">
        <div id="boxTasks">
          {{task.text}}
        </div>
          <button class="dellTasks" @click="DellitTasks(index , task.id)">🗑</button>
          
      </div>
      </div>
    </div>


</template>

<script>
export default {
  data(){
    return{
    name: 'App',
    newTasks:'',
    tasks:[],

};
},
methods:{
AddTasks(){
  if(this.newTasks.trim() !== ''){
    this.tasks.push({
      id: Date.now(),
      text: this.newTasks
    })
    this.newTasks = ''
  }
},
DellitTasks(index, id){
  const taskEl = document.getElementById(`task-${id}`)
  if(taskEl){
    taskEl.style.animation = 'deleteTasks 0.5s forwards'
    taskEl.addEventListener('animationend', () => {
      this.tasks.splice(index, 1)
    })
  }
}
}
};
</script>

<style >

@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap");
:root{
  --white:#ffffffea;
  --green:#d1e7dd;
  --blue:#84aafd;
  --tasks:rgb(47, 40, 255);
}

html{
  width:100%;
  height:100%;
}
body{
  width:100%;
  height:100%;
  background:var(--white);
  margin:0;
  color:var(--blue);
  font-family:'Poppins';
  color: var(--blue);
}
#App{
  display: grid;
  grid-template-columns:repeat(1,1fr);
  grid-template-rows:20% 80%;
  align-items: center;
  justify-content: center;
  justify-items: center;
  width:100%;
  height:100%;
}


#BoxApp{
  width:95%;
  height:95%;
  background:var(--green);
  display: flex;
  border:2px solid var(--blue);
  box-shadow:var(--blue) 2px 2px 4px;
  border-radius:15px;
  display: grid;
  grid-template-rows:15% 85%;
  align-items: center;

}
#UserTasks{
  height:3.2rem;
  width:100%;
  border-radius:10px;
  border:3px solid var(--blue);
  font-size:1.25rem;
  color:var(--blue);
  grid-row:1;
  grid-column:1;
  margin:2%;
}
p{
  font-size:5.5rem;
  
}
#AddTasks{
  width:10rem;
  height:3rem;
  border:2px solid var(--blue);
  border-radius:12px;
  grid-row:1;
  font-size:1.1rem;
  font-family:'Poppins';
  color: var(--blue);
  margin-left:10%;
  margin-top:5%;
}
#BoxApp2{
  width:100%;
  height:100%;
  overflow: scroll;
}
#section{
  display: grid;
  grid-template-columns:70% 30%;
}
#boxTasks{
  width:90%;
  height:5rem;
  background:var(--blue);
  display: flex;
  font-size:1.2rem;
  color:black;
  border:2px solid var(--tasks);
  border-radius:20px;
  margin:1%;
  align-items:center;
  grid-column:1;
}
.dellTasks{
  width:3rem;
  height:3rem;
  background: var(--blue);
  grid-column:2;
  border-radius:50%;
  border: 2px solid var(--tasks);
  font-size:2rem;
  align-content: center;
  justify-content: center;

}
.rowList{
  width:98%;
  height:20%;
  display:grid;
  grid-template-columns:80% 10% 10%;
  justify-content: center;
  align-content:center;
  align-items: center;
  transition:0.3s fadein;
  animation: fadein 0.6s ease forwards;

}
@keyframes fadein {
  0% {
    opacity:0.1;
  }
  50%{
    opacity:0.5;
  }
  100%{
  opacity:1;
  transform:translateY(5px);
  transform: translateX(5px);
  }
}
@keyframes deleteTasks {
  0%{
    opacity:1;
  }
  50%{
    opacity:0.7;
  }
  75%{
    opacity:0.4;
  }
  100%{
    opacity:0;
    visibility:hidden;
  }
}
@media(max-width:580px){
  #boxTasks{
    font-size:1rem;

  }
  #addTasks{
    width:6rem;
    height:3.2rem;
    font-size:1rem;
  }
}

</style>
