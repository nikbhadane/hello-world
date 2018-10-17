node{
      stage('Checkout'){
        checkout([$class: 'GitSCM', branches: [[name: '**']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '12345', url: 'https://github.com/nikbhadane/Chef_work']]])
        }
       
    buildStep('CI-execution'){
      stage('Build code'){
        echo 'Hello World Indianss'
        sh 'ls -al'
        sh 'df -h'
        sh 'cat /etc/passwd'
        sh 'cat README.md'
        sh 'sleep 45'
        }
	  stage('Test Code'){
	    sh 'echo "This goal is to verify stagesss"'
	    sh 'sleep 10'
      sh 'cat /etc/passwd'
	   }
     }
 }
void buildStep(String context, Closure closure) {
  stage(context);
  try {
    setBuildStatus(context, "In progress...", "PENDING");
    closure();
  } catch (e) {
    setBuildStatus(context, "Failure", "FAILURE");
    throw e
  }
  setBuildStatus(context, "Success", "SUCCESS");
}

// Updated to account for context
void setBuildStatus(String context, String message, String state) {
  context = context ?: "ci/jenkins/build-status"
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/nikbhadane/Chef_work"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: context],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
