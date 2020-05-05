#!groovy


@Library('jenkins-global-lib') _

import com.company.project.*
	deliveryPipeline{

def util = new com.company.project.util()




def notifySuccess() {
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
	}


node {
       checkout scm
	data = readYaml file: 'input.yaml'
     }


pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm 
            }
        }

	stage('Build the source code') {
            steps {
		script {
		     echo "Building the source code  ... "
		     util.buildSourceCode(data.App.name, data.App.name2.prop3, data.App.name2.prop4) 
		     commitMessage = util.getCommitMessage()

		}
		}
		}

	    stage ('Run the Unit Tests') {
	    	steps {
	    		script {
			        print "Executing the unit tests ... "
		     		util.executeUnitTests() 
			    }
	        }
	    }

	    stage ('Upload to Artifactory') {
	    	steps {
	    		script {
			        print "artifactory"
		     		util.uploadToArtifactory() 
			    }
	        }
	    }
        stage('Deploy to Servers') {
            steps {
	    		script {
		     		util.deploy() 
	        	}
            }
        }

}
	post {
        failure {
        	script {
        		notifyFailure()
        	}
        }
    }
}
	}
