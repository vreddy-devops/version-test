#!groovy
node ('master') {
	try {
		stage('Preparation') {
		  git branch: '$branch', url: 'git@github.com:vreddy-devops/version-test.git'
		  rtGradle.tool = "Gradle_35"
		  rtGradle.resolver repo:'repo', server: serverArti
		  rtGradle.useWrapper = false
   		}
	    stage('Version') {
	          dir('verifyJenkins') {

	        // env.VERSION_NAME = "7.5.0"
		      // sh 'pwd'
		       //sh 'll'
		        String readConfigFile = new File("verifyJenkins/gradle/configurations.gradle").text
		        def configLines = readConfigFile.readLines()
		        configLines.each { String line ->
        		    if (line.contains("versionName")) {
            			configVersion = line =~ /(\d+\.)(\d+\.)(\d+)/
            			println "CONFIG VER: = " + configVersion[0][0]
				        env.VERSION_NAME = configVersion[0][0]
        		    }
                    else {
                        env.VERSION_NAME = "7.5.0"
                    }
		        }
	        }
	    }

        stage('TestVersion') {
            
            dir('verifyJenkins') {
                sh """
                    test=${env.VERSION_NAME}
                    echo \$test
                """
            }
        }

    }
  catch (ex) {
        currentBuild.result = "FAILED"
        throw ex
    }
} 
