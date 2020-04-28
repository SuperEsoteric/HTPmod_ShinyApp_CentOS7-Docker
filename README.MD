# CentOS 7 Docker container with HTPmod Shiny App

A Shiny app for high-throughput data modeling and visualization of large-scale biological data in plants. Implemented on CentOS 7 with updates and tested in Docker Desktop for Windows on Windows 10 Hyper-V.  

Improvements over the existing implementations include migration to CentOS 7 and updated versions of components. User priviledges have been reduced when possible to improve security considerations when possible.  

https://github.com/htpmod/HTPmod  
https://github.com/htpmod/HTPmod-shinyApp

## Included packages:
    * HTPmod-ShinyApp
    * R
    * RStudio Server
    * Shiny-Server


## Instructions:
	1) Install Docker Desktop Community Edition: https://www.docker.com/products/docker-desktop
		a) For Windows 10:
		     i) Enable Hyper-V: https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v
		    ii) Install Docker Desktop for Windows: https://hub.docker.com/editions/community/docker-ce-desktop-windows

 	2) Clone or download this repository.

 	3) Build the Docker image from dockerfile using PowerShell prompt: 
		To access Shiny apps from host computer:
		    > docker build -f "%PathToYourFiles%\HTPmod-ShinyServer-CentosDockerfile" "%PathToYoursFiles%" --tag="htpmod-shiny" --no-cache
		To access Shiny apps from remote computers:
			> docker build -f "%PathToYourFiles%\HTPmod-ShinyServer-CentosDockerfile" "%PathToYoursFiles%" --tag="htpmod-shiny" --no-cache --build-arg HOST_HOSTNAME=$([System.Net.Dns]::GetHostByName(($env:computerName)).Hostname.toLower())

	4) Verify Docker image
		> docker images

	5) Run your HTPmod Shiny-Server Docker image
		> docker run -p 3838:3838 -p 8787:8787 -d htpmod-shiny
			+Shiny-Server is running at localhost:3838
			+RStudio Server is running at localhost:8787
			+username and password for RStudio Server is rstudio

	6) Accessing the Shiny app site: http://FQDN:3838/HTPmod/




## Modify the Docker Container
	> docker run -p 3838:3838 -p 8787:8787 -it HTpmod-shiny /bin/bash
		+Arg -i tells docker to attach stdin to the container.
		+Arg -t tells docker to give us a pseudo-terminal.
		+Arg /bin/bash will run a terminal process in your container.

## Adapted from:
	Centos 7 Docker Shiny-Server:
            https://github.com/keberwein/docker_shiny-server_centos7
                Provided by: Kris Eberwein
	            License: GNU General Public License v3.0
                https://github.com/keberwein/docker_shiny-server_centos7/blob/master/LICENSE
	HTPmod-shinyApp:
            https://github.com/htpmod/HTPmod-shinyApp
    	    Provided by: Chen Lab Computational Biology Group, School of Life Sciences, Nanjing University
	    	License: GNU General Public License v3.0
	        License URL: https://github.com/htpmod/HTPmod-shinyApp/blob/master/LICENSE
