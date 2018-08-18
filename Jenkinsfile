pipeline {
    agent any 
    //parameters {
       
         //string(defaultValue: "", description: 'Credencias da AWS', name: 'AWS_ACCESS_KEY_ID')
		 //string(defaultValue: "", description: 'Credencias da AWS', name: 'AWS_SECRET_ACCESS_KEY')
        //string(defaultValue: "", description: 'Credencias DockerHub', name: 'DOCKER_HUB_PASS')
    //}
    
    stages {      		

		stage('Build Aplicacao') { 
			steps {				
				echo "Building aplicacao com Gradle"
				sh "ls"
                //docker run --rm -v /opt/jenkins/workspace/deploy_app/:/codigo_da_aplicacao renatoadsumus/gradle:4.6"
               // sh "docker run --rm -v ${PWD}/docker-spring-sample/:/codigo_da_aplicacao renatoadsumus/gradle:4.6"							
			}			
		}
		
		
		stage('Build Imagem Docker da Aplicacao') { 
			steps {			
				echo "Gerando a Imagem Docker da Aplicacao"	
                ///sh "docker build -t renatoadsumus/docker-spring-sample ."			
				//sh "docker login --username=renatoadsumus --password=${DOCKER_HUB_PASS}"
                echo "### EXECUTANDO PUSH DA IMAGEM GERADA ###"
                //sh "docker push renatoadsumus/docker-spring-sample"               
                //sh "docker run --rm -e AWS_ACCESS_KEY_ID='${params.AWS_ACCESS_KEY_ID}' -e AWS_SECRET_ACCESS_KEY='${params.AWS_SECRET_ACCESS_KEY}' -e VERSAO='${env.BUILD_ID}' -e OPCAO='Novo' renatoadsumus/aws_cli:latest"
						
			}			
		}	

        stage('Run Aplicacao Local') { 
			steps {			
				echo "Gerando a Imagem Docker da Aplicacao"	
                //sh "docker run -d -p 8080:8080 renatoadsumus/docker-spring-sample"			
				//sh "docker run --rm -e AWS_ACCESS_KEY_ID='${params.AWS_ACCESS_KEY_ID}' -e AWS_SECRET_ACCESS_KEY='${params.AWS_SECRET_ACCESS_KEY}' -e VERSAO='${env.BUILD_ID}' -e OPCAO='Novo' renatoadsumus/aws_cli:latest"
						
			}			
		}

        stage('Run Aplicacao EB - AWS') { 
			steps {			
				echo "Gerando a Imagem Docker da Aplicacao"	                	
				//sh "docker run --rm -e AWS_ACCESS_KEY_ID='${params.AWS_ACCESS_KEY_ID}' -e AWS_SECRET_ACCESS_KEY='${params.AWS_SECRET_ACCESS_KEY}' -e VERSAO='${env.BUILD_ID}' -e OPCAO='Novo' renatoadsumus/aws_cli:latest"
						
			}			
		}	
        
    }
	
	//post {
	//	always {
	//	cleanWs()
	//	}
	//}
 }