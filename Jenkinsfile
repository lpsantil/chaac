retriever: modernSCM(
  [
    $class: "GitSCMSource",
    remote: "https://github.com/lpsantil/chaac.git"
  ]
)

openshift.withCluster() {
  env.NAMESPACE = openshift.project()
  env.APP_NAME = "${JOB_NAME}".replaceAll(/-build.*/, '')
  echo "Starting Pipeline for ${APP_NAME}..."
  env.BUILD = "${env.NAMESPACE}"
  env.DEV = "${APP_NAME}-dev"
  env.STAGE = "${APP_NAME}-stage"
  env.PROD = "${APP_NAME}-prod"
}

pipeline {
  // Use Jenkins Maven slave
  // Jenkins will dynamically provision this as OpenShift Pod
  // All the stages and steps of this Pipeline will be executed on this Pod
  // After Pipeline completes the Pod is killed so every run will have clean
  // workspace

  agent {
    label 'maven'
  }

  // Pipeline Stages start here
  // Requeres at least one stage
  stages {

    // Checkout source code
    // This is required as Pipeline code is originally checkedout to
    // Jenkins Master but this will also pull this same code to this slave

/*
    stage('Git Checkout') {
      steps {
        // Turn off Git's SSL cert check, uncomment if needed
        // sh 'git config --global http.sslVerify false'
        git url: "${APPLICATION_SOURCE_REPO}", branch: "${APPLICATION_SOURCE_REF}"
      }
    }
*/

    // Make chaac-builder bc, chaac is, chaac sa
    // Make chaac-deployer bc
    // Make chaac-passwd bc
    // Make chaac-reset bc
    // Make chaac-clean bc
    stage( 'Provisioner' )
    {
       steps
       {
          sh "oc apply -f templates/provision.yaml"
       }
    }
/*
    // Run chaac-builder bc
    stage( 'Builder' ){}
    // Run chaac-deployer bc,
    // Create new chaac-USER-dc, chaac-USER-svc, chaac-USER-rt,
    // Patch chaac-USER-dc 
    // Annotate chaac-USER-rt
    stage( 'Deployer' ){}
    // Set env chaac-USER-dc 
    stage( 'Password Updater' ){}
    // Set env chaac-USER-dc 
    stage( 'Password Reset' ){}
    // Delete chaac-USER-dc, chaac-USER-svc, chaac-USER-rt,
    stage( 'Cleaner' ){}
*/
  }
}
