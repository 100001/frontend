    var addHandlers = function(nodes){
       for(var i=0;i<nodes.length;i++){
          with({t:i}){
            nodes[t].onclick=function(){
               alert(t);
            }
          }
       }
    };