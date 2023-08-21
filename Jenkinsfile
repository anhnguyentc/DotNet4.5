def zipPath = "C:\\Program Files\\7-Zip\\7z.exe"
def packagePathService = "C:\\IT-VCBS\\BONPublish\\WEB\\"
def workspace = "C:\\Jenkins\\workspace"
def MSBUILD = "C:\\Jenkins\\lib\\MSBuild\\14.0\\Bin\\"

node{		
	stage("Checkout SCM"){
		cleanWs()
		checkout scm
	}
	
	stage ("Checkout soucecode"){
		bat """
			git clone -b master https://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@github.com/anhnguyentc/his-dvcongqgia-application.git %cd%
			if not exist \"%cd%\\BONPROJECT\\" mkdir %cd%\\BONPROJECT\\
			cd %cd% \\BONPROJECT\\
			git clone -b master https://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@github.com/anhnguyentc/his-dvcongqgia-application.git
			
			"""
			echo 'clone success'
	}

}