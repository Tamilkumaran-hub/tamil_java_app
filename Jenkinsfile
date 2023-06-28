@Library('my-shared-library') _

pipeline{
    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete\nchange', description: 'Choose create/Destroy')
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
        stage('Unit Test Maven'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
                    mvnTest()
		}
	    }
	}
        stage('Integration Test Maven'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
                    mvnIntegrationTest()
		}
	    }
	}
        stage('Static code analysis: Sonarqube'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
                    statiCodeAnalysis()
		}
	    }
	}
    }
}
