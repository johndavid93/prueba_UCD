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
            componentName: 'John',

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
                baseDir: '${WORKSPACE}',

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
}
     }
 

