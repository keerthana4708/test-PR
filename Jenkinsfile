build_agents = ["AMD-hipanl-nvidia-01","AMD-hipanl-vg20-01"]
buildmap =[:]
buildhip(node){
   return{
        stage("Source sync"){
           echo "sourec sync"
        }
        stage("build"){
            echo "Build"
        }

        stage("test") {
           echo "testimg"

        }


 }



}

node('BS5') { 
   for (node in build_agents) {
      buildmap[node] = buildhip(node)
   }

   buildmap['failFast']=false
   parallel  buildmap
}
