def secrets = [
    [path: params.VAULT_PATH_SVC_ACCOUNT_EPHEMERAL, engineVersion: 1, secretValues: [
        [envVar: 'OC_LOGIN_TOKEN', vaultKey: 'oc-login-token'],
        [envVar: 'OC_LOGIN_SERVER', vaultKey: 'oc-login-server']]],
    [path: params.VAULT_PATH_SVC_ACCOUNT_EPHEMERAL, engineVersion: 1, secretValues: [
        [envVar: 'OC_LOGIN_TOKEN_DEV', vaultKey: 'oc-login-token-dev'],
        [envVar: 'OC_LOGIN_SERVER_DEV', vaultKey: 'oc-login-server-dev']]],
    [path: params.VAULT_PATH_QUAY_PUSH, engineVersion: 1, secretValues: [
        [envVar: 'QUAY_USER', vaultKey: 'user'],
        [envVar: 'QUAY_TOKEN', vaultKey: 'token']]],
    [path: params.VAULT_PATH_RHR_PULL, engineVersion: 1, secretValues: [
        [envVar: 'RH_REGISTRY_USER', vaultKey: 'user'],
        [envVar: 'RH_REGISTRY_TOKEN', vaultKey: 'token']]],
]

def configuration = [vaultUrl: params.VAULT_ADDRESS, vaultCredentialId: params.VAULT_CREDS_ID, engineVersion: 1]

pipeline {
    agent {
        docker {
            image 'quay.io/cloudservices/cypress-e2e-image:06b70f3'
            label 'insights'
        }
    options {
        timestamps()
    }

    environment {
        PROJECT_NAME="insights-chrome"

        MASTER_BRANCH="master"
        MASTER_STABLE_BRANCH="master-stable"

        IMG_TAG=sh(script: "git rev-parse --short=8 HEAD", returnStdout: true).trim()
        NODE_BASE_IMAGE="registry.access.redhat.com/ubi9/nodejs-18:1-53"
        CYPRESS_TEST_IMAGE="quay.io/cloudservices/cypress-e2e-image:06b70f3"
    }

    stages {
        stage("Stage one") {
            steps {
                sh """
                    ls -lrt
                    pwd
                """
            }
        }
    }
}
