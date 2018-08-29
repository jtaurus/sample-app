node {
   
   def secrets = [
   [$class: 'VaultSecret', path: 'jakub-test/test', secretValues: [
     [$class: 'VaultSecretValue', envVar: 'testing', vaultKey: 'password']
   ]]]

   def configuration = [
     $class: 'VaultConfiguration',
     vaultUrl: 'http://127.0.0.1:8200/',
     vaultCredentialId: 'e1f904ca-40f7-49b0-a083-1014722b3462'   
   ]

   stage('Preparation') {
      git 'https://github.com/jtaurus/sample-app.git'
   }
   stage('Build') {
         wrap([$class: 'VaultBuildWrapper', configuration: configuration, vaultSecrets: secrets]) {
           sh 'echo "Attempting to authenticate"'
           sh 'php file.php $testing'
         }
         sh "cat file.txt"
   }
   stage('Results') {
      echo "done"
   }
}
