podTemplate(containers: [
    containerTemplate(
        name: 'maven', 
        image: 'maven:3.8.1-jdk-8', 
        command: 'sleep', 
        args: '30d',
        volumeMounts:
              name: 'maven-repo'
              mountPath: '/root/.m2/repository'         
        volumes:
              name: 'maven-repo'
              persistentVolumeClaim:
              claimName: 'jenkins-pv-claim'
        ),
  ]) {

    node(POD_LABEL) {
        stage('Get a Maven project') {
            git 'https://github.com/dlambrig/simple-java-maven-app.git'
            container('maven') {
                stage('Build a Maven project') {
                    sh '''
                    echo "maven build"
                    mvn -B -DskipTests clean package
                    '''
                    }
            }
        }
      }
     }  
