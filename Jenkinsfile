pipeline{
	agent any
	// agent {
	// 	docker {image 'node:alpine'}
	// }
	environment{
		dockerHome = tool 'myDocker'
		nodeHome = tool 'myNode'
		PATH = "$dockerHome/bin:$nodeHome/bin:$PATH"
	}
	stages{
		stage("A Stage"){
			steps{
				sh 'docker version'
				sh 'node -v'
				}
			}
        stage("Integration Stage"){
			steps{
				
				sh 'ls'
         
				}
			}
		stage("B Stage"){
				steps{
					echo "$PATH"
					echo "$env.BUILD_NUMBER"
					echo "$env.BUILD_ID"
					echo "$env.JOB_NAME"
					sh 'docker ps'
				}
			}	
		stage("C Stage"){
				steps{
					echo "C Stage"
					echo "hola..!"
				}
			}
        stage("Docker Build"){
				steps{
					script{
                        dockerImage = docker.build("indrajithvgp/jenkinsreactapp:${env.BUILD_NUMBER}")
                    }
				}
			}	
        stage("Docker Push"){
				steps{
					script{
                        docker.withRegistry('', dockerhub){
                            dockerImage.push()
                            dockerImage.push('latest')
                        }
                    }
				}
			}	
	}
	post{
		always{
			echo "always"
		}
		success{
			echo "success"
		}
		failure{
			echo "failure"
		}
	}
}	
