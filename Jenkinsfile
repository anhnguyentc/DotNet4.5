def zipPath = "C:\\Program Files\\7-Zip\\7z.exe"
def packagePathService = "C:\\IT-VCBS\\DOTNET45Publish\\"
def workspace = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\pipelineTest"
def MSBUILD = "C:\\Program Files (x86)\\MSBuild\\14.0\\Bin\\"

node{		
	stage("Checkout SCM"){
		cleanWs()
		checkout scm
	}
	
	stage ("Clone soucecode"){
		bat """
			git clone -b master https://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@github.com/anhnguyentc/DotNet4.5.git %cd%
			if not exist \"%cd%\\DOTNET45\\" mkdir %cd%\\DOTNET45\\
			cd %cd% \\DOTNET45\\
			git clone -b master https://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@github.com/anhnguyentc/DotNet4.5.git
			
			"""
			echo 'clone success'
	}
	
	stage ("Build soucecode"){
		bat """
		${MSBUILD}MSBuild.exe ${workspace}\\DOTNET45\\DotNet4.5\\WebApplication1.sln /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:SkipInvalidConfigurations=true /t:build /p:Configuration=Release /p:DeleteExistingFiles=True /p:publishUrl=${packagePathService}
			"""
	}

}