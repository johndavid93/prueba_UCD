node {
   step([$class: 'UCDeployPublisher',
        siteName: 'local',
        component: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
            componentName: 'Jenkins',
            createComponent: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',
                componentTemplate: '',
                componentApplication: 'Local'
            ],
            delivery: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Pull',
                pullProperties: 'FileSystemImportProperties/name=${BUILD_NUMBER}\nFileSystemImportProperties/description=Pushed from Jenkins',
                pullSourceType: 'File System',
                pullSourceProperties: 'FileSystemComponentProperties/basePath=C:\\Test',
                pullIncremental: false
            ]
        ]
    ])
}
