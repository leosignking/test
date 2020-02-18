node {
 	// Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project...'"
        	sh "gradle build --info"
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	            sh "gradle testClasses"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	            sh "gradle testClasses"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	            sh "gradle testClasses"
	        }
        }
      	stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
