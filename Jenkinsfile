node {
  checkout([$class: 'GitSCM', branches: [[name: '*']], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [[$class: 'SubmoduleOption', 
        disableSubmodules: false, 
        recursiveSubmodules: true, 
        reference: '', 
        trackingSubmodules: false], 
      [$class: 'MessageExclusion', 
        excludedMessage: '.*\\[(skip|ci)\\s+(skip|ci)\\].*']], 
        submoduleCfg: [], 
        userRemoteConfigs: 
        [[credentialsId: '647b503d-a3fa-4c17-88dd-ef48276d5d92', 
          url: 'git@github.com:Nava2/procsim-bld.git']]])

  withEnv(['MASTER_WORKSPACE=${env.WORKSPACE}']) {
    build job: './main',  parameters: [[$class: 'StringParameterValue', name: 'MASTER_WORKSPACE', value: env.WORKSPACE]]
  }
}