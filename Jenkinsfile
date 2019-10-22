#!groovy

node('master') {
    stage('Checkout') {
        checkout scm
    }
    
    stage('VAULT Connection Check') {
     def secrets = [
        [path: 'kv/campaign', engineVersion: 2, secretValues: [
            [envVar: 'vault_secret', vaultKey: 'campaign_user']]]
    ]

    // optional configuration, if you do not provide this the next higher configuration
    // (e.g. folder or global) will be used
    def configuration = [vaultUrl: 'http://ac-vault:8200',
                         vaultCredentialId: 'vault-id',
                         engineVersion: 2]
    // inside this block your credentials will be available as env variables
    withVault([configuration: configuration, vaultSecrets: secrets]) {
        sh 'echo $vault_secret'
        sh 'git -$vault_secret'
    }
        
    }
}
