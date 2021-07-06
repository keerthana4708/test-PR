
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

          stage("test") {
            echo "testimg"
 
        }
    }

 }

}

node('BS5') {
build_agents = ["AMD-hipanl-nvidia-01","AMD-hipanl-vg20-01"]
agents=[]
buildmap =[:]

for (agent in build_agents)  {
    def match = agent =~ /nvidia/
    if(!match){
      agents.add(agent)
    }

}

println "agents : $agents"
for (slave in agents) {
        buildmap[slave] = buildhip(slave)
   }

   buildmap['failFast']=false
   parallel  buildmap
}
