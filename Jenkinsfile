pipeline {
    agent any
    tools {
        maven 'MAVEN'
        jdk 'JAVA'
    }
    stages{
        stage('git url') {
            steps{
                git branch: 'master', url: 'https://github.com/mikey1967/game-of-life.git'
            }
        }

        stage('build') {
            steps{
                sh 'mvn clean install'
            }
        }

        stage('publish overs ssh') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible_server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'Dockerfile, hosts, mikey-dockerimage.yaml, mikey-dockercontainer.yaml, mikey-k8spod.yaml'), sshTransfer(cleanRemote: false, excludes: '', execCommand: '''ansible-playbook -i /opt/docker/hosts /opt/docker/mikey-dockerimage.yaml --limit 172.31.84.170
                ansible-playbook -i /opt/docker/hosts /opt/docker/mikey-dockercontainer.yaml --limit 172.31.86.136
                ansible-playbook -i /opt/docker/hosts /opt/docker/mikey-k8spod.yaml --limit 172.31.22.30''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: 'gameoflife-web/target', sourceFiles: 'gameoflife-web/target/*.war'), sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'mikey-pod.yaml, mikey-service.yaml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

                sshPublisher(publishers: [sshPublisherDesc(configName: 'kubernetes_server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//kubernetes', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'mikey-pod.yaml, mikey-service.yaml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}