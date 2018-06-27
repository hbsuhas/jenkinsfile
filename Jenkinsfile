node {
 	// Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
		
        	bat "echo 'checkout scm' for properties %prop_id% "
		def baseUrl= "http://localhost:3000/api/";
          
	
						try {
								def id =0;
								 if(isUnix())
								{
									id = $prop_id
								}
								else
								{
									id =prop_id
								}
								
							 def connectionProp = new URL(baseUrl+"v_jenkins_properties/"+id+"?column=ID")
                                    .openConnection() as HttpURLConnection
									
									if ( connectionProp.responseCode == 200 ) {
										
										def propjson =  new JsonSlurper().parseText(connectionProp.inputStream.text);
											
										println propjson;
																			
									  }
									
									else {
											
										println "Error in fetching jenkins_properties " + connectionProp.responseCode	
									
									}
									
							}
							catch(Exception e) {
									println e	
							}
        }
        stage ('Build') {
        	bat "echo 'shell scripts to build project...'"
        }
        stage ('Tests') {
	        parallel 'static': {
	            bat "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            bat "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            bat "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            bat "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
