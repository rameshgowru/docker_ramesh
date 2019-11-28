pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'This is to zip all files'
        
          zip archive: true, dir: '/demo', glob: '', zipFile: 'final'


      }
    }
   stage('DeployToRamesBox') {
            when {
                branch 'master'
            }
     
    
      steps {
       withCredentials([usernamePassword(credentialsId: 'rameshtest', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
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
                                        sourceFiles: 'final.zip',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'ls -l /tmp/abcd.zip'
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
