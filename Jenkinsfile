podTemplate(
    label: 'mypod',
    volumes: [
        emptyDirVolume(mountPath: '/etc/gitrepo', memory: false),
        hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
    ],
    containers:
    [
        containerTemplate(name: 'git', image: 'alpine/git', ttyEnabled: true, command: 'cat'),
        containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.0', command: 'cat', ttyEnabled: true),
        containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true
            //envVars: [secretEnvVar(key: 'DOCKER_HUB_PASSWORD', secretName: 'docker-hub-password', secretKey: 'DOCKER_HUB_PASSWORD')]
            )
        
    ]
)
{
    node('mypod') {
        stage('Clone repository') {
            container('git') {
                sh 'git clone -b test https://github.com/ssue96/eks-workshop-sample-api-service-go.git /etc/gitrepo'
            }
        }
        stage('Build and push docker image'){
            container('docker') {
                //ls -al
                //sh 'docker login -ualicek106 -p$DOCKER_HUB_PASSWORD'
                sh '''
                cd /etc/gitrepo
                pwd
                ls -al
                docker build -t eks-workshop .
                '''
                //sh 'docker push alicek106/kubernetes-python-sdk-example'
            }
        }
        stage('deploy') {
            container('kubectl') {
                sh '''
                #cd /etc/gitrepo/Jenkins
                cd /etc/gitrepo
                pwd
                ls -al
                #kubectl apply -f cluster-role-binding.yaml
                kubectl apply -f hello-k8s.yml
                kubectl get nodes
                kubectl get pods
                '''
            }
        }
    }
}
