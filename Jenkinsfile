#!groovy
node ('master') {
	try {
		stage('Preparation') {
		  git branch: 'master', url: 'git@github.com:vreddy-devops/version-test.git'
		  
   		}
	    stage('Version') {
	          dir('verifyJenkins') {  
		        File readConfigFile = new File('/var/lib/jenkins/workspace/test-version/verifyJenkins/gradle/configurations.gradle')
			 def configLines = readConfigFile.readLines()
		        configLines.each { 
			String line ->
        		    if (line.contains("versionName")) {
            			def configVersion = line =~ /(\d+\.)(\d+\.)(\d+)/
            			print "CONFIG VER: = " + configVersion[0][0]
		                env.VERSION_NAME = configVersion[0][0]
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
