node {

 
  stage('Preparation') { // for display purposes
     // Get some code from a GitHub repository
     git 'https://github.com/johndavid93/prueba_UCD.git'
  
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
