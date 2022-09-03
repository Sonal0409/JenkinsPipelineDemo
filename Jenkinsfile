pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    
    agent any
    
    stages{
        stage('Clone repo')
        {
            steps{
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        stage('Compile the code using maven')
        {
            steps{
                sh 'mvn compile'
            }
        }
        stage('Code review')
        {
            steps{
                sh 'mvn pmd:pmd'
            }
        }
         stage('Unit Testing')
        {
            steps{
                sh 'mvn test'
            }
        }
         stage('Code Coverage')
        {
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post{
                success{
                    cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                }
                
            }
        }
         stage('package')
        {
            steps{
                sh 'mvn package'
            }
        }
    }
}
