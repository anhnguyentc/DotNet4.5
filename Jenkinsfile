def zipPath = "C:\\Program Files\\7-Zip\\7z.exe"
def packagePathPublish = "C:\\IT-VCBS\\DOTNET45Publish\\"
def workspace = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\pipelineTest"
def MSBUILD = "\\MSBuild\\14.0\\Bin\\MSBuild.exe"
def NEXUS_USER = "jenkins"
def NEXUS_PASSWORD = "Nhim2023"
def NEXUS_ADD =  "http://192.168.1.40:8081"
def today = new Date()
def date = today.format("yyyyMMddHHmmss")
def FILE_PUBLISH = 'webtrading_' + date	+'.7z'
def publishWebDir = "C:\\Jenkins\\webtrading"

node{

	stage("Checkout SCM"){
		cleanWs()
		checkout scm
	}
	
	stage ("Clone soucecode"){
		bat """
			//git clone -b master https://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@github.com/anhnguyentc/DotNet4.5.git %cd%
			cd /d C:/Jenkins
			if not exist \"%cd%\\DOTNET45\\" mkdir %cd%\\DOTNET45\\
			cd %cd% \\DOTNET45\\
			if exist \"%cd%\\DotNet4.5\\" rmdir /s /q DotNet4.5			
			git clone -b master https://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@github.com/anhnguyentc/DotNet4.5.git
			
			"""
			echo 'clone success'
	}
	
	stage ("Build soucecode"){
		bat """
		cd /d C:/Jenkins/DOTNET45		
		\"C:\\Program Files (x86)\"${MSBUILD} C:\\Jenkins\\DOTNET45\\DotNet4.5\\WebApplication1.sln /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:SkipInvalidConfigurations=true /t:build /p:Configuration=Release /p:DeleteExistingFiles=True /p:publishUrl=${packagePathPublish}
			"""
	}
	
	stage ("Zip file Publish"){
		bat """
		cd /d ${packagePathPublish}
		dir
		del /F web.config
		\"${zipPath}\" a -r ${FILE_PUBLISH}
		
		"""
	
	}
	
	stage ("Push package to Nexus"){
		bat """
		cd /d ${packagePathPublish}
		curl --upload-file ${FILE_PUBLISH} -u ${NEXUS_USER}:${NEXUS_PASSWORD} ${NEXUS_ADD}/repository/raw-it-vcbs-hosted/ -k
		
		"""		
	} 
	
	def remote = [:]
    remote.name = 'test'
    remote.host = '192.168.1.177'
    remote.user = 'root'
    remote.password = 'Nhim2023@'
    remote.allowAnyHosts = true
    stage('Pull package from Nexus') {
      sshCommand remote: remote, command: """
	  cd /home/root/
      ansible-playbook -i inventory.ini --extra-vars "remote_dir='${publishWebDir}' nexus_url='${NEXUS_ADD}/repository/raw-it-vcbs-hosted/${FILE_PUBLISH}' nexus_user='${NEXUS_USER}' nexus_password='${NEXUS_PASSWORD}'"  pull-file-nexus.yaml
	  """
      //sshCommand remote: remote, command: "sh test.sh ${publishWebDir} ${NEXUS_ADD}/repository/raw-it-vcbs-hosted/${FILE_PUBLISH} ${NEXUS_USER} ${NEXUS_PASSWORD}"
    }	
	
	stage ("Unzip file Publish"){
		bat """
		cd /d ${publishWebDir}
		dir
		\"${zipPath}\" x ${FILE_PUBLISH} -o \"${publishWebDir}\" -y
		"""	
	}
		
}

/*node ('jenkins-slave-linux') {
	stage ("Ping server"){	
		echo "Ping server OK"
	}
} */