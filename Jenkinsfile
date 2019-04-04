pipeline {
    agent any 
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo
      stages {
         stage('Artifactory configuration'){
           steps {
              script {
                 rtMaven.tool ='Maven-3.5.3'
                 rtMaven.deployer releaseRepo: 'libs-release-local', 'libs-snapshot-local', server: server
                 rtMaven.resolver releaseRepo:'libs-release', snapshotRepo: 'libs-snapshot', server: server
                 rtMaven deployer.artifactDeploymentPatterns.addExclude("pom.xml")
                 buildInfo = Artifactory.newBuildInfo()
                 buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
                 buildInfo.env.capture = true
                 }
               }
           stage('Exute Maven'){
               steps {
                   script {
                       rtMaven.run pom: 'pom.xml' ,goals: 'clean install', buildinfo: buildInfo
                       }
                      }
                     }
           stage('Publish Build'){
               steps{
                   script {
                     server.publishBuildInfo buildinfo
                     }
                    } 
