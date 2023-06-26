pipeline{
	
	agent any
	
	stages{
		
		stage('Git Checkout'){
			
			steps{
				
				script{
					gitCheckout(
						branch: "main",
						url: "https://github.com/Tamilkumaran-hub/tamil_java_app.git"
					)
					
				}
			}
		}
	}
}
