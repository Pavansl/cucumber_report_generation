node
    {
        stage('Check Out')
        {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Pavansl/cucumber_report_generation.git']]])
            echo "current build number: ${currentBuild.number}"
            echo "previous build number: ${currentBuild.previousBuild.getNumber()}"
        }
        stage('Clean')
        {
          
            bat' mvn clean '
          
        }
        stage('Execuction of Test Suite')
        {
           
            bat 'mvn clean install -P dev '
           
        }
        stage('Cucumber Report')
        {
           
           cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', jsonReportDirectory: 'target/cucumber-report', pendingStepsNumber: -1, reportTitle: 'Cucumber_report', skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
          
        }
        stage('Mail')
        {
            emailext body: 'Check out, Execuction of Test Suite, Cucumber Report is finished', subject: 'Status', to: 'pavan.sl@ltts.com'
        }
    }
