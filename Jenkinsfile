node {
   step([$class: 'UCDeployPublisher',
        siteName: 'local',
        deploy: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$DeployBlock',
            deployApp: 'Jenkins',
            deployEnv: 'Test',
            deployProc: 'Deploy Jenkins',
            createProcess: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ProcessHelper$CreateProcessBlock',
                processComponent: 'Deploy'
            ],
            deployVersions: 'Jenkins:${BUILD_NUMBER}',
            deployOnlyChanged: false
        ]
    ])
}
