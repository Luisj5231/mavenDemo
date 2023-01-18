import groovy.json.*

node{
    properties([
        parameters([
            choice(name: 'env', choices: ['dev', 'perf', 'prod'], description: ''),
            booleanParam(name: 'Run', defaultValue: false,  description: ''),
            booleanParam(name: 'cleanWokspace', defaultValue: false,  description: ''),
            string(name: 'name', defaultValue: '', description: 'Nombre'),
        ])
    ])



    try {
        if(params.cleanWokspace){
            print("Limpiando Workspace....")
            deleteDir()
        }
        main()
    }
    catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
//export MAVEN_HOME='/opt/maven'
//export PATH='$PATH:$MAVEN_HOME/bin'
def mvnHome = tool name: 'maven-3.8.6', type: 'maven'
NEXUS_VERSION = "nexus3"
NEXUS_PROTOCOL = "http"
NEXUS_URL = "http://3.237.27.229:9181"
NEXUS_REPOSITORY = "maven-nexus-repo"
NEXUS_CREDENTIAL_ID = "nexus-cred"

def main(){
    stage("Clone code from VCS") {
        //sh 'git clone https://github.com/javaee/cargotracker.git'
        checkout([
            $class:'GitSCM',
            branches:[[name:'*/master']],
            userRemoteConfigs: [[url: 'https://gitlab.com/gevillegas/puebajenkinsselenium.git']]
        ])
    }
    dir('cargotracker'){
    stage('maven clean verify'){
        sh 'mvn clean verify'
    }


    /*stage("Publish to Nexus Repository Manager") {
        pom = readMavenPom file: "pom.xml";
        filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
        echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
        artifactPath = filesByGlob[0].path;
        artifactExists = fileExists artifactPath;
        if(artifactExists) {
            echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                nexusArtifactUploader(
                nexusVersion: NEXUS_VERSION,
                protocol: NEXUS_PROTOCOL,
                nexusUrl: NEXUS_URL,
                groupId: pom.groupId,
                version: pom.version,
                repository: NEXUS_REPOSITORY,
                credentialsId: NEXUS_CREDENTIAL_ID,
                artifacts: [
                    [artifactId: pom.artifactId,
                    classifier: '',
                    file: artifactPath,
                    type: pom.packaging],
                    [artifactId: pom.artifactId,
                        classifier: '',
                        file: "pom.xml",
                        type: "pom"]
                    ]
                );
        } else {
            error "*** File: ${artifactPath}, could not be found";
        }
    }*/
    }
}
