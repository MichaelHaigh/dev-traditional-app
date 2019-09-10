node() {
    git url: "https://phx-it-github-prod-1.eng.nutanix.com/michael-haigh/dev-traditional-app/", credentialsId: 'd8500ae9-87ba-4fdc-bf16-2535b0a51011'

    stage "Calm: Update App"
    step([$class: 'RunApplicationAction', actionName: 'UpdateApp', applicationName: 'dev-traditional-app', runtimeVariables: '{}'])
}
