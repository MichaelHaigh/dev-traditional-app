node() {
    git url: "https://github.com/MichaelHaigh/dev-traditional-app/", credentialsId: 'aea9e704-c6d6-4aae-91be-7243a5e7e850'

    stage "Calm: Update App"
    step([$class: 'RunApplicationAction', actionName: 'UpdateApp', applicationName: 'dev-traditional-app', runtimeVariables: '{}'])
}
