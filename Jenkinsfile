@Library('my-shared-library') _

pipeline{
    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
	string(name: 'ImageName', description: 'name of the docker image', defaultValue: 'javaapp')
	string(name: 'ImageTag', description: 'tag of the docker image', defaultValue: 'v1')
	string(name: 'DockerHubUser', description: 'user of the dockerhub', defaultValue: 'tamil001')
    }
    stages{
        stage('Git Checkout'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/Tamilkumaran-hub/tamil_java_app.git"
                    )
					
		}
	    }
	}
 //        stage('Unit Test Maven'){
 //        when { expression {  params.action == 'create' } }
 //            steps{
 //                script{
 //                    mvnTest()
	// 	}
	//     }
	// }
 //        stage('Integration Test Maven'){
 //        when { expression {  params.action == 'create' } }
 //            steps{
 //                script{
 //                    mvnIntegrationTest()
	// 	}
	//     }
	// }
 //        stage('Static code analysis: Sonarqube'){
 //        when { expression {  params.action == 'create' } }
 //            steps{
 //                script{
	// 	    def SonarQubecredentialsId = 'sonar'
 //                    statiCodeAnalysis(SonarQubecredentialsId)
	// 	}
	//     }
	// }
 //        stage('Quality gate status: Sonarqube'){
 //        when { expression {  params.action == 'create' } }
 //            steps{
 //                script{
	// 	    def SonarQubecredentialsId = 'sonar'
 //                    QualityGateStatus(SonarQubecredentialsId)
	// 	}
	//     }
	// }
	stage('Maven build: Maven'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
		    mvnBuild()
		}
	    }
	}
	stage('Docker image build'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
		    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
		}
	    }
	}
	stage('Docker Image Scan: Trivy'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
		    dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
		}
	    }
	}
	stage('Docker Image Push: Dockerhub'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
		    dockerImagePush("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
		}
	    }
	}
	stage('Docker Image Cleanup: Dockerhub'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
		    dockerImageCleanup("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
		}
	    }
	}
    }
}
