def zipPath = "C:\\Program Files\\7-Zip\\7z.exe"
def packagePathPublish = "C:\\IT-VCBS\\DOTNET45Publish\\"
def workspace = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\pipelineTest"
def MSBUILD = "\\MSBuild\\14.0\\Bin\\MSBuild.exe"
def NEXUS_USER = "jenkins"
def NEXUS_PASSWORD = "Nhim2023"
def NEXUS_ADD =  "http://localhost:8081"
def FILE_PUBLISH = "packagePathPublish.7z"

node{		
	stage("Checkout SCM"){
		cleanWs()
		checkout scm
	}
		
	stage ("Ping server"){
		steps {				
				ansiblePlaybook credentialsId: 'ansible-credentials', inventory: 'Ansible/inventory/production/group_vars/web_servers.yml', playbook: 'Ansible/playbooks/ping_server.yml.yml'
            }		
	}

}