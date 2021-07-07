
def buildhip(slave){
     return{
        node(slave) {
          stage("Source sync"){
            dir("${WORKSPACE}/hip"){
               checkout scm
               }
            dir("${WORKSPACE}/hipamd") {
              git branch: 'amd-master',
              url: 'ssh://gerritgit/compute/ec/hipamd'
            }
         }
          stage("build"){
             echo "Build"
           }
            
         println "${env.NODE_NAME}"
       
         //def matches = "${env.NODE_NAME}" =~/nvidia/
         //println "matches =  $matches"
          
         for (a in agents) {
          if ("${env.NODE_NAME}" == a)  {   
             stage("rocm-dev installation"){
                echo "dev instalation"
            }
         }else {
              println "Nvidia is found"
          }   
         }
          stage("test") {
            echo "testing"
 
        }
    }

 }

}

timestamps {
     node('BS5') {
     build_agents = ["AMD-hipanl-nvidia-01","AMD-hipanl-vg20-01"]
     buildmap =[:]
     agents = []


     for (agent in build_agents)  {
        def match = agent =~ /nvidia/
        if(!match){
             agents.add(agent)
         }

      }   
     
     println "agents = $agents"
     for (slave in build_agents) {
        buildmap[slave] = buildhip(slave)
     }

     buildmap['failFast']=false
     parallel  buildmap
  }//closing the node
}//closing the timestamps
