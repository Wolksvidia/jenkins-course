//Jenkinsfile examples code

//example code to input 
userInput = input(id: 'userInput',    
    message: 'Choose an environment',    
    parameters: [
        [$class:'ChoiceParameterDefinition', choices: "Dev\nQA\nProd", name: 'Env']
                ]  
)
chooseOptions = input(id: 'chooseOptions',
    message: 'Select options',    
    parameters: [                           
        [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Option A'],    
        [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Option B'],
        [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Option C']
    ]   
)
stage('Input') { //si nadie apreta el boton de proceder dentro de 60 minutos el stage falla
  timeout(60) {
    input 'Keep going?'
  }
  //timeout(time: 60 units: 'MINUTES')
  //[NANOSECONDS, MICROSECONDS, MILLISECONDS, SECONDS, MINUTES, HOURS,DAYS]
}
//condicionales
if (userInput.Env == "Dev") {
  // deploy dev stuff
} else if (userInput.Env == "QA"){
  // deploy qa stuff
} else {
  // deploy prod stuff
}

// stage que se procesan en paralelo
stage('Deploy to all environments'){
  parallel(
    dev: (    
      node('deploy') {
        // code
      }
    ),
    qa: (
      node('deploy') {
        // code
      }
    ),
    prod: (
      node('deploy') {
        // code
      }
    )
  )
}


try {      
  node('testing') {
    // testing code goes here -- calling scripts, maven, etc
  } catch (err) {
   input(         
       id: 'testFailed', message: 'Test failed! Proceed anyway?', ok: 'Proceed'        
      )      
  }
}
//funcion para mensajes a slack
def notify(channel,text) {  
  slackSend (channel: "${channel}", message: "${text}", teamDomain: "$YOURTEAMDOMAIN", token: "$YOURSLACKTOKEN")  
}
notify("#deployments", "@here Another successful pipeline run for   ${env.JOB_NAME}")