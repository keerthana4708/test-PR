build_agents = ["AMD-hipanl-nvidia-01","AMD-hipanl-vg20-01"]
buildmap =[:]

buildhip(agent){
   return{
      node(agent) {
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



}

node('BS5') { 
   for (agent in build_agents) {
      buildmap[agent] = buildhip(agent)
   }

   buildmap['failFast']=false
   parallel  buildmap
}
