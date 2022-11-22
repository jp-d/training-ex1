pipeline {
  agent any

  options {
    ansiColor("xterm")
    disableConcurrentBuilds()
  }
  
  environment {
    
	// --> Variable used within the pipeline
    // VARIABLE_EXAMPLE = "a value"

  }
  
  parameters {
    string(name: "input_word", defaultValue: "word", trim: true, description: "Input word")
  }
  
  stages {
    stage('Treatment') {
      steps {
        script {
		  appUpdateStart = time.getCurrTime()
		  styling.printInfo("################## Chrono => Treatment stage start ${appUpdateStart} ##################")
		  compterNbVoyelles(%input_word%)	  
		  styling.printInfo("################## Chrono => Treatment stage ended at ${time.getCurrTime()} ##################")
		}
      }	  
	}
	stage('Conditional treatment') {
      steps {
        script {
          appBuildStart = time.getCurrTime()
		  styling.printInfo("################## Chrono => Application build stage start ${appBuildStart} ##################")
		  
		  
          styling.printInfo("################## Chrono => Application build started at ${appBuildStart} and ended at ${time.getCurrTime()} ##################")
        }
      }
    }
  }

}

def compterNbVoyelles(mot) {
    def nbVoyelles = 0
    for (i = 0; i < mot.length; i++) {
        def lettre = mot[i].toLowerCase()
        if ((lettre === "a") || (lettre === "e") || (lettre === "i") || (lettre ==="o") || (lettre === "u") || (lettre === "y")) {
            nbVoyelles = nbVoyelles + 1
        }
    }
    return nbVoyelles
}
