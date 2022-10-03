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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd devsecops/vulnerable/staging && docker-compose up -d  && sleep 40 && docker rm -vf staging_VulnerableApp-facade_1 staging_VulnerableApp-php_1 staging_VulnerableApp-jsp_1 staging_VulnerableApp-base_1', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'devsecops/vulnerable/staging', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
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
