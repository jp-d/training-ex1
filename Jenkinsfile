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
    stage('Treatment') {
      steps {
        script {
          appUpdateStart = time.getCurrTime()
          styling.printInfo("################## Chrono => Treatment stage start ${appUpdateStart} ##################")
          NB_VOYELLES = compterNbVoyelles(%input_word%)
          styling.printInfo("NB_VOYELLES : ${NB_VOYELLES}")  
          styling.printInfo("################## Chrono => Treatment stage ended at ${time.getCurrTime()} ##################")
        }
      }	  
    }
    stage('Treatment 2') {
      steps {
        script {
          appBuildStart = time.getCurrTime()
          styling.printInfo("################## Chrono => Treatment 2 start ${appBuildStart} ##################")
		  
		  
          styling.printInfo("################## Chrono => Treatment 2 ended at ${time.getCurrTime()} ##################")
        }
      }
    }
  }

}

def compterNbVoyelles(mot) {
    def nbVoyelles = 0
    for (i = 0; i < mot.length(); i++) {
        def lettre = mot[i].toLowerCase()
        if ((lettre == "a") || (lettre == "e") || (lettre == "i") || (lettre =="o") || (lettre == "u") || (lettre == "y")) {
            nbVoyelles ++
        }
    }
    return nbVoyelles
}

