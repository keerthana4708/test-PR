build_agents = ["AMD-hipanl-nvidia-01","AMD-hipanl-vg20-01"]
buildmap =[:]

buildhip(slave){
   return{
      node(slave) {
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
   for (slave in build_agents) {
      buildmap[slave] = buildhip(slave)
   }

   buildmap['failFast']=false
   parallel  buildmap
}
