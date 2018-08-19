pipeline {
    agent any 
      
    stages {      		

	//stage('Git Clone Teste Funcional'){
      //      steps{
        //        git branch: 'master',
                    
          //          url: 'https://github.com/renatoadsumus/docker-spring-sample-test.git'                   
            //}
        //}

		stage('Build e Analise Codigo') { 
			steps {				
				echo "Building aplicacao com Gradle"							
                sh "docker run --rm -v /opt/jenkins/workspace/deploy_app/:/codigo_da_aplicacao renatoadsumus/gradle:4.6"
               
			   // sh "docker run --rm -v ${PWD}:/codigo_da_aplicacao renatoadsumus/gradle:4.6"							
			}			
		}

		stage('Analise Log') { 
			steps {

				echo "Analisando Logs em busca de erro 500 e 503"	
			}

		}
		
		
		stage('Build Imagem Docker da Aplicacao') { 
			steps {			
				echo "Gerando a Imagem Docker da Aplicacao"	
                sh "docker build -t renatoadsumus/docker-spring-sample ."			
				sh "docker login --username=renatoadsumus --password=${DOCKER_HUB_PASS}"
                echo "### EXECUTANDO PUSH DA IMAGEM GERADA ###"
                sh "docker push renatoadsumus/docker-spring-sample"               
                //sh "docker run --rm -e AWS_ACCESS_KEY_ID='${params.AWS_ACCESS_KEY_ID}' -e AWS_SECRET_ACCESS_KEY='${params.AWS_SECRET_ACCESS_KEY}' -e VERSAO='${env.BUILD_ID}' -e OPCAO='Novo' renatoadsumus/aws_cli:latest"
						
			}			
		}	

		stage('Teste Funcional') { 
			steps {

				echo "Analise Sonar"	
			}

		}

        stage('Run Aplicacao Local') { 
			steps {			
				echo "Gerando a Imagem Docker da Aplicacao"	
                sh "docker run -d -p 8080:8080 renatoadsumus/docker-spring-sample"			
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