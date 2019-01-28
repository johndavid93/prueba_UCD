// comment
pipeline {
 agent any
 stages {
        stage('Checkout-git'){
               steps{
		git poll: true, url: 'git@github.com:TestDevops/Jenkinsfile.git'
               }
        }
        stage('CreateVirtualEnv') {
            steps {
				sh '''
					bash -c "virtualenv entorno_devops && source entorno_devops/bin/activate"
				'''

            }
        }
        stage('InstallRequirements') {
            steps {
            	sh '''
            		bash -c "source ${WORKSPACE}/entorno_devops/bin/activate && ${WORKSPACE}/entorno_devops/bin/python ${WORKSPACE}/entorno_devops/bin/pip install -r requirements.txt"
                '''
            }
        }   
        stage('TestApp') {
            steps {
            	sh '''
            		bash -c "source ${WORKSPACE}/entorno_devops/bin/activate &&  cd src && ${WORKSPACE}/entorno_devops/bin/python ${WORKSPACE}/entorno_devops/bin/pytest && cd .."
                '''
            }
        }  
        stage('RunApp') {
            steps {
            	sh '''
            		bash -c "source entorno_devops/bin/activate ; ${WORKSPACE}/entorno_devops/bin/python src/main.py &"
                '''
            }
        } 
        stage('BuildDocker') {
            steps {
            	sh '''
            		docker build -t apptest:latest .
                '''
            }
        } 
    stage('PushDockerImage') {
            steps {
            	sh '''
            		docker tag apptest:latest mijack/apptest:latest
					docker push mijack/apptest:latest
					docker rmi apptest:latest
                '''
            }
        } 
 
 stage('DEPLOY_UCD') {
            steps {
                echo "[EXEC] - Construyendo script de despliegue"
                //writeFile file: 'deploy.sh', text: "mqsideploy IIBDESA -e SVR_AFP -a ${PROJECT}.bar -w 1200;"
                echo "[EXEC] - Despliegue sobre Urban Code Deploy ";
                war warFile: "${soccer-1.0}.war", glob: 'dist/**/*, ScriptDeploy/**/*'

                step([
                        $class:'UCDeployPublisher',
                        siteName :"${URBAN_PRD_APP}",
                        component: [
                        $class:'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
                            componentName:"${soccer-1.0}",
                                createComponent: [

                                        $class:'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',
                                        componentTemplate:'TEMPLATE-PORTAL-FRONT-WAR',
                                        componentApplication:'Fidaval'
                                ],

                                delivery:[

                                        $class:'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Push',
                                        pushVersion:"1.${BUILD_ID}",
                                        baseDir:"${workspace}",
                                        fileIncludePatterns: "${FILE_WAR_PATTERN}",
                                        fileExcludePatterns: '',
                                        pushProperties     : "war-file-name=soccer-1.0",
                                        pushDescription    : 'Pushed from mpipeline-ppopular-backend Jenkins Job'
                                ]
                        ]
                ])

 
}
    
}
}

