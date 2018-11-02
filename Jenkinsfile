#!groovy
node {
	label ('master') 
}
	try {
	    stage('Version') {
	          dir('verifyJenkins') {

	        // env.VERSION_NAME = "7.5.0"
		      // sh 'pwd'
		       //sh 'll'
		        String readConfigFile = new File("gradle/configurations.gradle").text
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
            
            dir('https-saiteja1141-gmail.com-scm-tma-genesis-android') {
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
