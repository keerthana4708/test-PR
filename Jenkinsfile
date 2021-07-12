
def buildhip(slave){
     return{
        node(slave) {
          stage("Source sync"){
            dir("${WORKSPACE}/hip"){
               checkout scm
               }
            dir("${WORKSPACE}/hipamd") {
              git branch: 'develop',
              url: 'https://github.com/ROCm-Developer-Tools/hipamd'
            }
            dir("${WORKSPACE}/ROCm-OpenCL-Runtime-internal") {
               git branch:'develop'
               url : 'https://github.com/RadeonOpenCompute/ROCm-OpenCL-Runtime-internal'

            }
            dir("${WORKSPACE}/ROCclr") {
               git branch:'develop'
               url : 'https://github.com/ROCm-Developer-Tools/ROCclr-internal'

            }
            dir("${WORKSPACE}/HIP-Common") {
               git branch:'develop'
               url : 'https://github.com/ROCm-Developer-Tools/HIP-Common'
                
            }



         }
          stage("build"){
             dir("${WORKSPACE}/ROCclr"){
                nproc = sh (script: "nproc",returnStdout: true).trim()
                OPENCL_DIR = "${WORKSPACE}/ROCclr"
                sh(script: """export $OPENCL_DIR;mkdir -p build; cd build; cmake -DAMD_OPENCL_PATH="$OPENCL_DIR" -DCMAKE_INSTALL_PREFIX=/opt/rocm/rocclr ..; make -j${nproc}""")

             }
            dir("${WORKSPACE}/HIP-Common"){
               HIP_DIR = "${WORKSPACE}/HIP-Common"
               sh(script: """export ${HIP_DIR}; mkdir -p build; cd build; make -DHIP_AMD_BACKEND_SOURCE_DIR="$HIPAMD_DIR" -DCMAKE_PREFIX_PATH="/opt/rocm/" ..;make -j${nproc} """ )    
            
             }
 
           }
            
         println "${env.NODE_NAME}"
          
          stage("test") {
            echo "testing"
 
        }
    }

 }

}

timestamps {
     node('BS5') {
     labels = ["nvidia-ext", "amd-ext"]
     buildmap =[:]
     agents = []


     for (agent in labels)  {
        def match = agent =~ /nvidia/
        if(!match){
             agents.add(agent)
         }

      }   
     
     println "agents = $agents"
     for (slave in labels) {
        buildmap[slave] = buildhip(slave)
     }

     buildmap['failFast']=false
     parallel  buildmap
  }//closing the node
}//closing the timestamps
