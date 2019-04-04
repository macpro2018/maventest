    pipeline {
    agent any
        stages {
        stage ('Build') {
             git url: 'https://github.com/cyrille-leclerc/multi-module-maven-project'
             withMaven(
                maven: 'M3',
                mavenSettingsConfig: 'my-maven-settings',
                 }
                 }
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

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: MAVEN_TOOL, // Tool name from Jenkins configuration
                    pom: 'maven-example/pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
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
