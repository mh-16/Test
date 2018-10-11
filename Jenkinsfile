#!/usr/bin/env groovy

node ('master')
{
    stage 'Checkout code'
        git 'https://github.com/mh-16/Test.git'
    stage 'Nuget'
       bat 'C:/Tools/nuget.exe restore SeleniumNUnitParam.sln -source "https://www.nuget.org/api/v2/"'
    stage 'Build'
        bat "\"${tool 'msbuild'}\" SeleniumNUnitParam.sln /p:Configuration=debug /p:platform=\"Any CPU\" /p:ProductVersion=1.0.0.${BUILD_NUMBER}"
    stage 'Update'
		bat 'npm install -g chromedriver'
	stage 'Test'
        bat 'C:/Tools/Nunit/nunit3-console.exe SeleniumNUnitParam\\bin\\Debug\\SeleniumNUnitParam.dll xml=testresult.xml'
		
	stage("PublishTestReport")
		nunit testResultsPattern: 'TestResult.xml'
     
    
}