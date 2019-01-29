node {  
         stage('Preparation') { // for display purposes
     // Get some code from a GitHub repository
     git 'https://github.com/johndavid93/prueba_UCD.git'
  }

        stage('Desplegar en UCD'){

// clase: define el plugin Pipeline para definir. El nombre de clase del complemento UCD Jenkins Pipeline es UCDeployPublisher
   step([$class: 'UCDeployPublisher',

// siteName: El nombre del servidor de IBM UrbanCode Deploy configurado en la página Configurar sistema de Jenkins.
        siteName: 'UCD_DEPLOY',

// Especifique acciones para realizar contra un solo componente.
        component: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',

// componentName: define el nombre del (nuevo) componente en IBM UrbanCode Deploy.
            componentName: 'JD',

// createComponent: define un nuevo componente para crear.
            createComponent: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',

// componentTemplate: el nombre de una plantilla para basar el componente.
                componentTemplate: '',

// componentApplication: el nombre de una aplicación a la que se agrega el componente.
                componentApplication: ''
            ],

// entrega: Realizar una importación de la versión del componente.
            delivery: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Push',

// pushVersion: Nombre para asignar la versión del componente. Jenkins resuelve BUILD_NAME.
                pushVersion: '${BUILD_NUMBER}',

// baseDir: el directorio base que contiene los artefactos de compilación.
                     //baseDir: '${WORKSPACE}',
               baseDir: '/var/lib/jenkins/workspace/UCD_Jenkinsfile',

// fileIncludePatterns: Regex que define qué archivos incluir.
                fileIncludePatterns: '**/*',

// fileExcludePatterns: Regex que define qué archivos excluir.
                fileExcludePatterns: '',

// pushProperties: Asigna propiedades a la nueva versión del componente. Sintaxis: KEY = VALUE separado por nuevas líneas.
                pushProperties: '',

// pushDescription: Descripción para asignar a la versión del componente.
                pushDescription: ''
   ]
                 ]
            ])
                 /////////////Desplegar componente
                  step([$class: 'UCDeployPublisher',
        siteName: 'UCD_DEPLOY',
        component: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
            componentName: 'JD',
        ],
                 deploy: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$DeployBlock',

// deployApp, deployEnv y deployProc: la aplicación, el entorno y el proceso de aplicación que se ejecutarán.
            deployApp: '',
            deployEnv: '',
            deployProc: '',

// deployReqProps: Especifique las propiedades del proceso de la aplicación.
            deployReqProps: 'AppProcessProp1=Value1\nAppProcessProp2=Value2',

// createProcess: Si el proceso de la aplicación no existe, esta especificación creará una.
            createProcess: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ProcessHelper$CreateProcessBlock',

// processComponent: especifique un proceso de un solo componente para inicializar el nuevo proceso de aplicación. Creará un solo paso Importar componente en un proceso de solicitud basado en el componente especificado anteriormente.
                processComponent: ''
            ],

// deployVersions: Especifique qué versiones implementar. Sintaxis: COMPONENTE: VERSION. Separe el múltiplo con un nuevo carácter de línea (\ n).
            deployVersions: 'Jenkins:${BUILD_NUMBER}',

// deployOnlyChanged: especifique que solo se implemente en versiones modificadas.
            deployOnlyChanged: false,

// createSnapshot: crea una instantánea del entorno de implementación. 
// Si deployWithSnapshot es verdadero, la instantánea se creará primero y se usará para la implementación. 
// Además, si deployWithSnapshot es verdadero, las Versiones de implementación en el bloque de implementación se agregarán a la nueva instantánea, en lugar de usarse para la implementación.
            createSnapshot: [
               $class:'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$CreateSnapshotBlock',
                snapshotName: '',
                deployWithSnapshot: false
                      ]
                          ]
                        ])
     /*
                 /////////////////Importación de la versión del disparador
                  step([$class: 'UCDeployPublisher',
        siteName: 'UCD_DEPLOY',

// Crear un nuevo componente.
        component: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
            componentName: 'JD1',
            createComponent: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',
                componentTemplate: '',
                componentApplication: ''
            ],
                   delivery: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Pull',

// pullProperties Propiedades para dar a cada versión del componente. Sintaxis: PLUGINComponentProperties / PROPERTY = VALUE. Separe cada definición de propiedad con un nuevo carácter de línea (\ n).
                pullProperties: 'FileSystemImportProperties/name=${BUILD_NUMBER}\nFileSystemImportProperties/description=Pushed from Jenkins',

// pullSourceType: el nombre de la configuración de origen.
                pullSourceType: 'File System',

// pullSourceProperties: propiedades específicas de la configuración de origen especificada. Sintaxis: PLUGINComponentProperties / PROPERTY = VALUE. Separe cada definición de propiedad con un nuevo carácter de línea (\ n).
                pullSourceProperties: 'FileSystemComponentProperties/basePath=C:\\Test',

// pushIncremental: Las importaciones de IBM UrbanCode Deploy solo importarán los cambios de la versión anterior.
                pushIncremental: false
                  
         ]
  ]    
                        ])
                 */
}
     }
 

