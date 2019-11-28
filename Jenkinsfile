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
                                        sourceFiles: 'demo/**/*',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'ls -l /tmp/ ; pwd ; ps -ef|grep java ; cd /tmp/demo/; ls -lcrt'
                                        execCommand: 'netstat -anp|grep java'

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
