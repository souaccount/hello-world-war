pipeline {
	agent none
        stages {
           stage ("tomcat buid & move to other node") {
	     agent {label "slave_server1"}
           	steps {
                      sh 'sudo mvn package'
		      sh 'ls'
		      sh 'scp -R target/hello-world-war-1.0.0.war juser3@172.31.2.244:/opt/tomcat/webapps'
		      echo "sucessfully copied build to other node"
	      	}
	   }
	   stage ('diploy in node2') {
	      agent {label "slave_server2"}
	   	steps {
			sh 'sudo chmod -R 777 /opt'
			sh 'sudo sh /opt/tomcat/bin/shutdown.sh'                   
                        sh 'sudo sleep 3'
                        sh 'sudo sh /opt/tomcat/bin/startup.sh'
                        echo "diployment is sucessfull"
                        echo "copy the public ip of instace and open it in browser with port:8090"
		}
	   } 	   
        }
}
