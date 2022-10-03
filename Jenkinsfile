pipeline{
    agent any

    tools{
        gradle 'Gradle'
        }

    stages {
        stage('Build') {
            steps {
                    // for build
                    sh './gradlew clean build --no-daemon'

                    
        }
        }
      
        stage('peformance test'){
            steps {
                    // for unit testing
                    junit(testResults: 'build/test-results/test/*.xml', allowEmptyResults : true, skipPublishingChecks: true)
          }
        }

        stage ('staging') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
            }
        }

//         stage ('Prod-approval') {
//             steps {
//                 input "Deploy to prod?"
//             }
//         }

//         stage ('production') {
//             steps {
//                 sshPublisher(publishers: [sshPublisherDesc(configName: 'docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd devsecops/vulnerable/production && docker-compose up -d', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'devsecops/vulnerable/production', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
//             }
//         }

    }
}
