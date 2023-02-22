pipeline {
  agent any

  options {
    ansiColor("xterm")
    disableConcurrentBuilds()
  }
  
  environment {
    // --> Variable used within the pipeline
    // just to test
    NB_VOYELLES = 0
  }
  
  parameters {
    string(name: "input_word", defaultValue: "soleil", trim: true, description: "Input word")
    //choice(name: 'input_word', choices: ['Soleil', 'Tornade', 'Extraordinairement'], description: 'Input word choice')
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
          //printInfo("Selected word: " + params.input_word)
          printInfo("################## Chrono => Treatment 2 ended at ${getCurrTime()} ##################")
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

// Main function coloring a string message
def printColor(message = '', foreground = 'black', background = 'white', style = 'none'){
    def Map foregroundCodes = [black: '30', red: '31', green: '32', yellow: '33', blue: '34', magenta: '35', cyan: '36', white: '37']
    def Map backgroundCodes = [black: '40', red: '41', green: '42', yellow: '43', blue: '44', magenta: '45', cyan: '46', white: '47']
    def Map styleCodes = [none: '0', bold: '1', lowIntensity: '2', underline: '3']
    try {
        String fgd = foregroundCodes[foreground]
        String bgd = backgroundCodes[background]
        String st = styleCodes[style]
        String colorCode = fgd + ';' + st + ';' + bgd + 'm'
        println('\033[' + colorCode + message + '\033[0m')
    }
    catch(Exception e){
        println("/!\\ Error in coloring message ${message} \n--> Exception: ${e}")
    }
}

// Coloring string functions by message level
def printInfo(message){
    printColor(message, 'blue', 'white', 'bold')
}

def printNote(message){
    printColor(message, 'magenta', 'white', 'bold')
}

def printError(message){
    printColor(message, 'red', 'white', 'bold')
}

def printWarning(message){
    printColor(message, 'yellow', 'white', 'bold')
}

def printSuccess(message){
    printColor(message, 'green', 'white', 'bold')
}

def now () {
  return new Date()
}

def getCurrTime() {
  return now().format("dd-MM-yy_HH:mm:ss", TimeZone.getTimeZone('Europe/Paris'))
}

