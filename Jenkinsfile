node {
  checkout([$class: 'GitSCM', branches: [[name: '*']], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [[$class: 'SubmoduleOption', 
        disableSubmodules: false, 
        recursiveSubmodules: true], 
      [$class: 'MessageExclusion', 
        excludedMessage: '.*\\[(skip|ci)\\s+(skip|ci)\\].*']], 
    userRemoteConfigs: 
      [[credentialsId: '647b503d-a3fa-4c17-88dd-ef48276d5d92', 
        url: 'git@github.com:Nava2/procsim-bld.git']]])

  def MASTER_WORKSPACE = env.WORKSPACE 

  def ALL_OS = ['trusty', 'osx' ] // OS.Win64]
  def ALL_CONFIGS = ['Debug', 'Release']

  checkout([$class: 'GitSCM', branches: [[name: '*']], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [[$class: 'SubmoduleOption', 
        disableSubmodules: false, 
        recursiveSubmodules: true, 
        reference: '', 
        trackingSubmodules: false], 
      [$class: 'RelativeTargetDirectory', 
        relativeTargetDir: './${env.GIT_BRANCH}/'],
      [$class: 'MessageExclusion', 
        excludedMessage: '.*\\[(skip|ci)\\s+(skip|ci)\\].*']], 
        submoduleCfg: [], 
        userRemoteConfigs: 
        [[credentialsId: '647b503d-a3fa-4c17-88dd-ef48276d5d92', 
          url: 'git@github.com:Nava2/hc12sim.git']]])
  

  def buildTrusty = {
    CONFIGS.each { config -> 
      ['clang', 'gcc'].each { compiler ->
        ws("os/${os}/compiler/${compiler}/config/${config}") {
          dir(env.MASTER_WORKSPACE) {
            echo "Configuring ${os}/${compiler}/${config}"
            sh '''\
              cd ${MASTER_WORKSPACE}
              vagrant ssh trusty <<EOM
                sudo use-${compiler}
                source /opt/qt56/bin/qt56-env.sh 

                cd ~vagrant/workspace
                mkdir -p build/${compiler}/${config}
                cd build/${compiler}/${config}

                cmake ../../../ -GNinja -DVERBOSE=1 -DCMAKE_BUILD_TYPE=${config}
              EOM'''
          }
        }
      }
    }
  }

  ALL_OS.each { os ->
      echo "Bringing up os: ${os}"
      try {
        dir(env.MASTER_WORKSPACE) {
            sh "vagrant up ${os}"
        }

        switch ( os ) {
            case 'trusty':
                buildTrusty()
                break;
            case 'osx':
                break;
            case 'win64':
                break;
        }
      } catch (err) {
        currentBuild.result = 'FAILURE'
      } finally {
        dir(env.MASTER_WORKSPACE) {
            sh "vagrant destroy ${os}"
        }
      }
  }

  dir(env.MASTER_WORKSPACE) {
      sh 'vagrant destroy -f '
  }
}