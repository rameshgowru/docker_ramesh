pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'This is to zip all files'
        
            // Write an useful file, which is needed to be archived.
    writeFile file: "demo/usefulfile.txt", text: "This file is useful, need to archive it."

    // Write an useless file, which is not needed to be archived.
    writeFile file: "demo/uselessfile.md", text: "This file is useless, no need to archive it."
        
      }
    }
   stage('DeployToRamesBox') {
         
     
    
      steps {
       withCredentials([usernamePassword(credentialsId: 'test', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'rameshtest',
                                sshCredentials: [
                                    username: "$USERNAME",
                                    encryptedPassphrase: "$USERPASS"
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: '*',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'ls -l /tmp/'
                                        execCommand: 'ps -ef|grep java'
                                        execCommand: 'cd /tmp/demo/'
                                        execCommand: 'ls -lart'
                                    )
                                ]
                            )
                        ]
                    )
              

      }
    }

  
}
}
}
