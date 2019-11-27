https://docs.rstudio.com/shiny-server/

#### Install R and Shiny R Packages

$ sudo yum install R

$ sudo su - \
-c "R -e \"install.packages('shiny', repos='https://cran.rstudio.com/')\""

### Download Shiny Server

$ sudo wget https://download3.rstudio.org/centos6.3/x86_64/shiny-server-1.5.9.923-x86_64.rpm

### Install Shiny Server

$ sudo yum install --nogpgcheck shiny-server-1.5.9.923-x86_64.rpm

### Start, Stop, Restart 

$ sudo systemctl start shiny-server

$ sudo systemctl kill -s HUP --kill-who=main shiny-server --> reload, keep all current connection