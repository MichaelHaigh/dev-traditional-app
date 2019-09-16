def tasks = [:]
git url: "https://github.com/MichaelHaigh/dev-traditional-app/", credentialsId: 'aea9e704-c6d6-4aae-91be-7243a5e7e850'

tasks["traditional"] = {
    stage ("Calm: Update Traditional App") {
        node() {
            step([$class: 'RunApplicationAction', actionName: 'UpdateApp', applicationName: 'dev-traditional-app', runtimeVariables: '{}'])
        }
    }
}

tasks["hybrid"] = {
    stage ("Calm: Update Hybrid App") {
        node("docker") {
            env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()

            stage "Build"
            def devdockerapp = docker.build "michaelatnutanix/dev-docker-app"
    
            stage "Publish"
            devdockerapp.push 'latest'
            devdockerapp.push "${env.GIT_COMMIT}"
    
            stage "Deploy"
            step([$class: 'RunApplicationAction', actionName: 'UpdateApp', applicationName: 'dev-hybrid-app', runtimeVariables: '''{
                "label": "${env.GIT_COMMIT}"
            }'''])
        }
    }
}

parallel tasks
