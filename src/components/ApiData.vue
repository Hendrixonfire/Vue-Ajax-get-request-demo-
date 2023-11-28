<template>
    <div>
        <h1> Ajax Get Demo</h1>
        <button type="button" class="imageButton" id="glow-on-hover" @click="loadDoc()">Change Content</button>
       <div class="flow">
        <div id="ajaxDemo">  
          <h2>Name:</h2>
        </div>
          <div id="ajaxDemoTwo" >  
           <h2>Phone:</h2>
        </div>
         <div id="ajaxDemoThree" >  
           <h2>Picture:</h2>
           
        </div>
        </div>
        
    </div>
    
    </template>


<script> 
import axios from "axios";

export default {
    data(){
        return {
            obj: [],
            objTwo: [],
            data: '',
            index: 0,
        };
    },
   
    methods: {

        loadDoc() {
        const xhr = new XMLHttpRequest();
        xhr.onload = function() {
            if (xhr.status == 200){
                console.log("success");
                this.data = JSON.parse(this.response);
                console.log(this.data);

                function getName(item){
                return item.name.first + item.name.last;
            }
                function getEmail(item){
                return item.phone;
            }
                function getPicture(item){
                    return item.picture.thumbnail;
                }
               
                this.obj = this.data.results.map(getName);
                this.objTwo = this.data.results.map(getEmail);
                this.objThree = this.data.results.map(getPicture);
                console.table(this.obj);
                   console.table(this.objTwo);
                       console.table(this.objThree);
                   
                     document.getElementById("ajaxDemo").innerHTML += "<p>" + this.obj + "</p>" ;
                   
        
                     document.getElementById("ajaxDemoTwo").innerHTML +=  "<p>" + this.objTwo + "</p>" ;  
               
                    
               
                 
                   
                    const node = document.createElement("img");
                    node.classList.add("ajaxDemoThree")
                    document.getElementById("ajaxDemoThree").appendChild(node).src = this.objThree;  
                    
                 
            }   
            
            }            
        xhr.open("GET", "https://randomuser.me/api/", true);
        xhr.send();
    }

    
  
    }
};






</script>

