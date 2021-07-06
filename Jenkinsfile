
def buildhip(slave,backend){
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
          if(backend==0) {
             stage("rocm-dev installation"){
                echo "dev instalation"
            }
          else {
             println "nvidia is found"
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
backend =0

for (slave in build_agents) {
        def match = slave =~ /nvidia/
        if(match){
            backend =1
            buildmap[slave] = buildhip(slave,backend)
        }
   }

   buildmap['failFast']=false
   parallel  buildmap
}
}
