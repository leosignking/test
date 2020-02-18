node {
 	// Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project...'"
        	sh "./gradlew build --info"
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	            sh "./gradlew testClasses"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	            sh "./gradlew testClasses"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	            //sh "gradle testClasses"
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
