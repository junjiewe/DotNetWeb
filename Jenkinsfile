node {
	
	stage('Checkout') {

			git 'https://github.com/junjiewe/DotnetWeb.git'

	}

	stage('Nuget') {
		bat '"C:\ProgramData\chocolatey\bin\nuget.exe" restore HelloWeb/HelloWeb.sln'
	}

	stage('Build') {

		powershell '''

			cd "C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Community\\MSBuild\\Current\\Bin\\"

			.\\MSBuild.exe "C:\\Users\\610169\\Desktop\\DotNetWeb\\HelloWeb\\HelloWeb.sln" /p:Configuration=Release

		'''

	}

	stage('Test') {

		powershell '''

			cd "C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Community\\Common7\\IDE\\Extensions\\TestPlatform"

			.\\VSTest.Console.exe "C:\\Users\\610169\\Desktop\\DotNetWeb\\HelloWeb\\HelloWeb.Tests\\bin\\Debug\\HelloWeb.Tests.dll"

		'''

	}

	stage('SonarQube analysis'){

		withSonarQubeEnv('SonarQube') { 

		

		powershell '''

			cd "C:\\Users\\610169\\Documents\\sonar-scanner-4.2.0.1873-windows\\bin"

			.\\sonar-scanner.bat -X -D sonar.projectKey=twoPipeline -D sonar.projectName=DotNetHelloWeb -D sonar.projectVersion=2.0 -D sonar.login=admin -D sonar.password=admin -D sonar.projectBaseDir="C:\\Users\\610169\\Desktop\\DotNetWeb\\HelloWeb\\" -D sonar.visualstudio.solution="HelloWeb.sln"

		'''

		}

	}

}