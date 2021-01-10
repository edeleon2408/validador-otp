// comment
pipeline {
 agent any
 stages {
    /*stage('Checkout-Project'){     
    	 steps{
            echo 'Revisando repositorio del Proyecto'
			git branch: 'develop', poll: true, url: 'https://github.com/edeleon2408/validador-api-otp.git'
         }        	
    }*/
    stage('Clean-Install-Packages'){     
    	 steps{
            echo 'Limpiando e Instalando paquetes del Proyecto'
            bat """
                      call cd admin-otp
                      call dir
                      call npm install 
		      call npm run ng -- build --prod
		      call dir
                """
	   }        	
    }
    stage('Unit-Test'){     
    	 steps{
            echo 'Realizando pruebas unitarias del proyecto'
	   /* bat """
                      call cd admin-otp
		      call npm run ng -- test
                    """	*/
	 }        	
    }
    stage('SCA-SonarQ'){     
    	 steps{
            echo 'Realizando escaneo del proyecto'
			
	   }        	
    }
    stage('Build-Project'){     
    	 steps{
            echo 'Construyendo Binario o Imagen del Proyecto'
	    bat """
                      call cd admin-otp
		      call docker build -f docker/Dockerfile -t admin-otp .
		      call docker tag admin-otp docker-registry-default.apps.claro.co/dev-motor-autenticacion/admin-otp:1.0
		      call docker images
		      call cd docker
		      call docker-compose up -d
		      call docker ps
                """				
	 }        	
    }
    stage('Deploy-Artifactory'){     
    	 steps{
            echo 'Realizando despliegue del binario o imagen al servidor de Artefactos'	
	    /*bat """	
	    	      call oc login https://consoleapi.claro.co:443 --token=k-2caPuuiHbsEL0kb5uchspcwsuw8lngkNXJxV_PPsx4
		      call docker login -u ECM09447F -p XILKm8Ckdw5CiD4xUc1KaZtaaKH8fFxthWwwKeXVesM docker-registry-default.apps.claro.co
            	      call docker push docker-registry-default.apps.claro.co/dev-motor-autenticacion/admin-otp
		"""*/
	 }        	
    }//fin stage
    
  }//fin stages
  
  post {
        success {
            echo 'I will success!'
            //mail bcc: '', 
            //body: "<b>Notificación CI</b><br><br>Estimado Usuario, El proceso CI se ha ejecutado de manera satisfactoria.<br><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}",
            //cc: '', 
            //charset: 'UTF-8', 
            //from: '', 
            //mimeType: 'text/html', 
            //replyTo: '', 
            //subject: "SUCCESS CI: Project name -> ${env.JOB_NAME}", 
            //to: "edeleon2408@gmail.com";  
                     
        }
        failure {
        	echo 'I will failure!'
            //mail bcc: '', 
            //body: "<b>Notificación CI</b><br><br>Estimado Usuario, El proceso CI ha fallado, por favor notificar al area administrativa del proceso.<br><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}",
            //cc: '', 
            //charset: 'UTF-8', 
            //from: '', 
            //mimeType: 'text/html', 
            //replyTo: '', 
            //subject: "FAILURED CI: Project name -> ${env.JOB_NAME}", 
            //to: "edeleon2408@gmail.com";
        }
    }//fin post
}
