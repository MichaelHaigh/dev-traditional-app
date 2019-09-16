def tasks = [:]

tasks["traditional"] = {
    stage ("Calm: Update Traditional App") {
        node("traditional") {
            git url: "https://github.com/MichaelHaigh/dev-traditional-app/", credentialsId: 'aea9e704-c6d6-4aae-91be-7243a5e7e850'
            step([$class: 'RunApplicationAction', actionName: 'UpdateApp', applicationName: 'dev-traditional-app', runtimeVariables: '{}'])
        }
    }
}

tasks["hybrid"] = {
    stage ("Calm: Update Hybrid App") {
        node("docker") {
            docker.withRegistry('', 'bef9483a-47b8-4096-9bce-bc0cdd198b9a') {
                git url: "https://github.com/MichaelHaigh/dev-traditional-app/", credentialsId: 'aea9e704-c6d6-4aae-91be-7243a5e7e850'
                env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()

                echo "Docker Build"
                def devdockerapp = docker.build "michaelatnutanix/dev-docker-app"
    
                echo "Docker Publish"
                devdockerapp.push 'latest'
                devdockerapp.push "${env.GIT_COMMIT}"
    
                echo "Deploy"
                step([$class: 'RunApplicationAction', actionName: 'UpdateApp', applicationName: 'dev-hybrid-app', runtimeVariables: '''{
                    "label": "${env.GIT_COMMIT}"
                }'''])
            }
        }
    }
}

parallel tasks
