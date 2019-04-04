    pipeline {
    agent any
        tools {
    maven 'Maven'
    }
        stages {
        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "test-1",
                    url: "https://champ25.jfrog.io/champ25",
                    username: "admin",
                    password: "Ee0Bd2Hr2Cb3Gi"
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "ARTIFACTORY_SERVER",
                    releaseRepo: "libs-release-local",
                    snapshotRepo: "libs-snapshot-local"
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "ARTIFACTORY_SERVER",
                    releaseRepo: "libs-release",
                    snapshotRepo: "libs-snapshot"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "ARTIFACTORY_SERVER"
                )
            }
        }
    }
}
