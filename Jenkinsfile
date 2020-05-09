#!groovy


@Library('jenkins-global-lib') _

import com.company.project.*
def util = new com.company.project.util()

def AgentName='Windows_10_Agent'
def anyBuildFailed='false'

/*def notifySuccess() {
		emailext (
			subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			body: '${JELLY_SCRIPT, template="html"}',
			mimeType: 'text/html',
			to: "vallab.v@gmail.com",
			from: "DevOps <devops.local.smtp@gmail.com>",
			replyTo: "vallab.v@gmail.com",
			//recipientProviders: [[$class: 'DevelopersRecipientProvider']]
		)
	}

	def notifyFailure() {
		emailext (
			subject: "Failure: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			body: '${JELLY_SCRIPT, template="html"}',
			mimeType: 'text/html',
			to: "vallab.v@gmail.com",
			from: "DevOps <devops.local.smtp@gmail.com>",
			replyTo: "vallab.v@gmail.com",
			//recipientProviders: [[$class: 'DevelopersRecipientProvider']]
		)
	}

	def emailDownloadLink(String artifactUrl) {
		emailext (
			subject: "Build Release: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			body: "URL: $artifactUrl",
			mimeType: 'text/html',
			to: "vallab.v@gmail.com",
			from: "DevOps <devops.local.smtp@gmail.com>",
			replyTo: "vallab.v@gmail.com",
			//recipientProviders: [[$class: 'DevelopersRecipientProvider']]
		)
	}  */


/* node {
       checkout scm
	data = readYaml file: 'input.yaml'
     } */


pipeline {
    agent none
	 options {
		 skipDefaultCheckout() // Don't checout automatically
		}

    stages {
        stage('Build Preparation') {
            agent { label "${AgentName}"  }
				steps {
						script {
							deleteDir()
							checkout scm
							echo "Checkout is complete"
							bat 'git clone "https://github.com/vinssm/CommonRepo.git"'
						}
                   }
              }

	stage('Build') {
        agent { label "${AgentName}"  }
			steps {
				script {
					Component_details = readYaml file: 'NewSampleApplication\\input.yaml'
					env.AssemblyVersioning = "${Component_details.App.AssemblyPath}"
					for (String item_entry : AssemblyVersioning.split() ) {
						env.AssemblyVersioning=item_entry
						echo "##### ${BUILD_NUMBER}  ######################"
						echo "##### ${WORKSPACE}  ######################"
						echo "##### ${AssemblyVersioning}  ######################"
						echo "##### ${CommitNumber}  ######################"
					}
					
				}
			}
		}
	}
}



	  /*  stage('Run the Unit Tests') {
	    	steps {
	    		script {
			        print "Executing the unit tests ... "
		     		util.executeUnitTests() 
			    }
	        }
	    }   */

	   /* stage ('Upload to Artifactory') {
	    	steps {
	    		script {
			        print "artifactory"
		     		util.uploadToArtifactory() 
			    }
	        }
	    }   */


      /*  stage('Deploy to Servers') {
            steps {
	    		script {
		     		util.deploy() 
	        	}
            }
        } 
} 


/*	post {
        failure {
        	script {
        		notifyFailure()
        	}
        }
    }
}

  */
