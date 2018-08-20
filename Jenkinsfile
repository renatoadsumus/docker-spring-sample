pipeline {
    agent any 
      
	 parameters {
    choice(
        name: 'TipoDeploy',
        choices: "PrimeiroDeploy\nDeployRecorrente",
        description: 'Validacao e Deploy na AWS' 
		)
  }

    stages { 	

		stage('Build e Analise Codigo') { 
			steps {				
				echo "Building aplicacao com Gradle"							
                sh "docker run --rm -v /opt/jenkins/workspace/deploy_app/:/codigo_da_aplicacao renatoadsumus/gradle:4.6"
               			  							
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
               
						
			}			
		}	        

       stage('Deploy - EB AWS') { 
			steps {			
				echo "Gerando a Imagem Docker da Aplicacao"	                	
				 sh "docker run --rm -v /opt/jenkins/workspace/deploy_app/eb/:/opt/artefato_deploy -e AWS_ACCESS_KEY_ID='${AWS_ACCESS_KEY_ID}' -e AWS_SECRET_ACCESS_KEY='${AWS_SECRET_ACCESS_KEY}' -e VERSAO='${env.BUILD_ID}' -e OPCAO='${params.TipoDeploy}' renatoadsumus/aws_cli:1.0"
						
			}						
		}  	
	
	post {
		always {
		cleanWs()
		}
	}
 }