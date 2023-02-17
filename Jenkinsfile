pipeline {
  agent any

  options {
    ansiColor("xterm")
    disableConcurrentBuilds()
  }
  
  environment {
    // --> Variable used within the pipeline
    NB_VOYELLES = 0
}
  
  parameters {
    string(name: "input_word", defaultValue: "soleil", trim: true, description: "Input word")
  }
  
  stages {
    stage('Treatment 1') {
      steps {
        script {
          appUpdateStart = getCurrTime()
          printInfo("################## Chrono => Treatment 1 start ${appUpdateStart} ##################")
          NB_VOYELLES = compterNbVoyelles(params.input_word)
          printInfo("NB_VOYELLES : ${NB_VOYELLES}")  
          if (NB_VOYELLES >= 5 ) {
            env.TRIGGER = "ON" 
            printInfo("TRIGGER: " + env.TRIGGER)
          } else {
            env.TRIGGER = "OFF" 
          }
          printInfo("################## Chrono => Treatment 1 ended at ${getCurrTime()} ##################")
        }
      }	  
    }
    stage('Treatment 2') {
      when { expression { env.TRIGGER == "ON" } }
      steps {
        script {
          appBuildStart = getCurrTime()
          printInfo("################## Chrono => Treatment 2 start ${appBuildStart} ##################")
		  
		  
          printInfo("################## Chrono => Treatment 2 ended at ${getCurrTime()} ##################")
        }
      }
    }
  }
