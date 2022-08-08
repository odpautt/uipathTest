pipeline {
   agent any
   environment {
	MAJOR = '1'
	MINOR = '0'
	//Orchestrator Services
	UIPATH_ORCH_URL = https://netvm-prpa34.epmtelco.com.co/
	UIPATH_ORCH_LOGICAL_NAME =
	UIPATH_ORCH_TENANT_NAME = Production
	UIPATH_ORCH_FOLDER_NAME = INDRA
   }

   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
         }
      }
     
     
      stage('Hola') {
         steps {
            echo 'Hola Mundo'
         }
      }
 
   }
}
