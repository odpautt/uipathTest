pipeline {
	    agent any
	

	        // Environment Variables
	        environment {
			
			  //nodo_RPA = "netfvm-psonar02"
			  //se indica la url del repositorio
			  git_url = "https://github.com/odpautt/uipathTest.git"

			  // el branch indicado puede ser (Desarrollo,Test,preproduccion,master)
			  branch = "test"

			  //se indican las credenciales establecidas para el acceso a git 
			  credentialsId = "95422137"
	        
				MAJOR = '1'
				MINOR = '0'
				//Orchestrator Services
				UIPATH_ORCH_URL = "https://netvm-prpa34.epmtelco.com.co/"
				UIPATH_ORCH_LOGICAL_NAME = ""
				UIPATH_ORCH_TENANT_NAME = "Desarrollo"
				UIPATH_ORCH_FOLDER_NAME = "INDRA"
			}
	

	    stages {
		
		//stage('Version_Control') {
		//		steps {
		//			//node("${env.nodo_RPA}") {
		//			git url: "${env.git_url}", branch: "${env.branch}", credentialsId: "${env.credentialsId}"
		//		//}
		//   }
		//}
	        

	        // Printing Basic Information
	        stage('Preparing'){
	            steps {
	                
    	                echo "Jenkins Home ${env.JENKINS_HOME}"
    	                echo "Jenkins URL ${env.JENKINS_URL}"
    	                echo "Jenkins JOB Number ${env.BUILD_NUMBER}"
    	                echo "Jenkins JOB Name ${env.JOB_NAME}"
    	                echo "GitHub BranhName ${env.BRANCH_NAME}"
    	            
	            }
	        }
	

	         // Build Stages
	        stage('Build') {
	            steps {
	                
    	                echo "Building..with ${WORKSPACE}"
    	                UiPathPack (
    	                      outputPath: "Output\\${env.BUILD_NUMBER}",
    	                      projectJsonPath: "project.json",
    	                      version:[$class: 'ManualVersionEntry', version: "${MAJOR}.${MINOR}.${env.BUILD_NUMBER}"],
    	                      useOrchestrator: false,
    						  traceLevel: "None"
    				                )
	                
	            }
	        }
	         // Test Stages
	        stage('Test') {
	            steps {
	                echo 'Testing..the workflow...'
	            }
	        }
	

	         // Deploy Stages
	        stage('Deploy to UAT') {
	            steps {
	                
    	                echo "Deploying ${BRANCH_NAME} to UAT "
    	                UiPathDeploy (
    	                packagePath: "Output\\${env.BUILD_NUMBER}",
    	                orchestratorAddress: "${UIPATH_ORCH_URL}",
    	                orchestratorTenant: "${UIPATH_ORCH_TENANT_NAME}",
    	                folderName: "${UIPATH_ORCH_FOLDER_NAME}",
    	                environments: "DEV",
    	                credentials: [$class: 'UserPassAuthenticationEntry', credentialsId: 'APIUserKey1'],
						//credentials: Token(accountName: "${UIPATH_ORCH_LOGICAL_NAME}", credentialsId: 'APIUserKey'), 
    					traceLevel: "None",
    					entryPointPaths: 'Main.xaml'
    					)
	                	
	            }
	        }
	

	

	   //      // Deploy to Production Step
	   //     stage('Deploy to Production') {
	   //         steps {
	   //             echo 'Deploy to Production'
	   //             }
	   //         }
	   // }
	

	   // // Options
	   // options {
	   //     // Timeout for pipeline
	   //     timeout(time:80, unit:'MINUTES')
	   //     skipDefaultCheckout()
	   // }
	

	

	   // // 
	   // post {
	   //     success {
	   //         echo 'Deployment has been completed!'
	   //     }
	   //     failure {
	   //       echo "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.JOB_DISPLAY_URL})"
	   //     }
	   //     always {
	   //         /* Clean workspace if success */
	   //         cleanWs()
	   //     }
	    }
	

	}