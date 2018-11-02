#!groovy
node ('master') {
	try {
		stage('Preparation') {
		  git branch: 'master', url: 'git@github.com:vreddy-devops/version-test.git'
		  
   		}
	    stage('Version') {
	          dir('verifyJenkins') {  
			// def readConfigFile = readFile "gradle/configurations.gradle"
		        File readConfigFile = new File('/var/lib/jenkins/workspace/test-version/verifyJenkins/gradle/configurations.gradle')
			 def configLines = readConfigFile.readLines()
			//  println configLines
		        configLines.each { 
			String line ->
        		    if (line.contains("versionName")) {
				println versionName
            			//configVersion = line =~ /(\d+\.)(\d+\.)(\d+)/
            		//	print "CONFIG VER: = " + configVersion[0][0]
		        //	env.VERSION_NAME = configVersion[0][0]
				    //String config_ver = configVersion[0][0]
				      //  envVars.put(VERSION_NAME,config_ver)
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
