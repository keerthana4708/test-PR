
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
          if(slave in agents) {
             stage("rocm-dev installation"){
                echo "dev instalation"
            }
         
          }else {
             println "nvidia is found"
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

for (buildSlave  in build_agents) {
    def match = buildSlave =~ /nvidia/
    if (match) {
         agents.add(buildSlave)
}

println "agents $agents"

for (slave in build_agents) {
        buildmap[slave] = buildhip(slave)
   }

   buildmap['failFast']=false
   parallel  buildmap
  }
 }
}
