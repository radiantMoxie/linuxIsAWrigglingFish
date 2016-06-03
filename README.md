#Linux Server Configuration
In this final project for Udacity's Full Stack Web Developer Nanodegree, I deployed a web application that I had developed earlier in the program. Udacity and Amazon provided me a virtual server in Amazon'a Elastic Compute Cloud (EC2).

**IP Address:** 52.40.239.99
**SSH Port:** 2200
**URL**: http://ec2-52-40-239-99.us-west-2.compute.amazonaws.com

###Summary of Software Installed 
* **apache2**: _HTTP Server, Version 2.4.7-1ubuntu4.9_
* **libapache2-mod-wsgi**: _hosts Python applications on Apache2 server, Version 3.4-4ubuntu2.1.14.04.2_
* **postgresql**: _Postgresql Database server, Version 9.3+154ubuntu1_
* **git**: _Version control system tools, Version 1:1.9.1-1ubuntu0.3_
* **python-setuptools**: _An easy-install package to facilitate installing Python packages, Version 3.3-1ubuntu2_
* **sqlalchemy**: _ORM and SQL tools for Python, Version 1.0.13_
* **flask**: _Microframework for web applications, Version 0.11_
* **psycopg2**: _PostgreSQL adapter for Python, Version 2.4.5_
* **oauth2**: _Authorization framework for third-party login (Google and Facebook), Version 1.9.0.post1_
* **requests**: _HTTP library for Python, Version 2.2.1_

###Summary of Configurations Made and Third-Party Resources Used
[This walkthrough](https://github.com/stueken/FSND-P5_Linux-Server-Configuration) was vital for me. I discovered it through the Udacity forums late in the game and it was a great way for me to feel that I was on the right track! Also the recommended resources from the assignment: [Project 5 Resources](https://discussions.udacity.com/t/project-5-resources/28343), [p5 How I Got Through It](https://discussions.udacity.com/t/p5-how-i-got-through-it/15342), [markedly-underwhelming-and-potentially-wrong-resource-list-for-p5](https://discussions.udacity.com/t/markedly-underwhelming-and-potentially-wrong-resource-list-for-p5/8587)

1. Created a new user named `grader`, ensured user had strong password, granted this user `sudo` permissions, configured user to authenticate using Amazon-provided `RSA` keys [(Great starting point from Digital Ocean)](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-12-04) [(Exploring 'permission denied public key' error)](http://serverfault.com/questions/39733/why-do-i-get-permission-denied-publickey-when-trying-to-ssh-from-local-ubunt) [(Udacity discussion re: copying RSA keys)](https://discussions.udacity.com/t/not-able-to-login-using-grader-login/161357/3)
2. Configured prompting of password for `sudo` command use every 15 minutes [(Password prompting for sudo)](http://askubuntu.com/questions/636092/how-to-get-sudo-to-prompt-you-for-a-password-each-time )
3. Disabled login of root user
3. Updated and upgraded all currently installed packages [(Should you always restart when it tells you to?)](http://askubuntu.com/questions/258297/should-i-always-restart-the-system-when-i-see-system-restart-required)
4. Configured local timezone to UTC [(Clear instructions for switch to UTC)](https://help.ubuntu.com/community/UbuntuTime#Using_the_Command_Line_.28terminal.29)
5. Changed SSH port from default 22 to 2200
6. Configured the UFW to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123) [(UFW config)](https://help.ubuntu.com/community/UFW)
7. Added new host `127.0.0.1 ip-10-20-17-144 grader` to `/etc/hosts` to resolve warning message `sudo: unable to resolve host ...` when `sudo` executed [(Helpful AWS Forum)](https://forums.aws.amazon.com/thread.jspa?threadID=104765)
8. Installed Apache2 Webserver,`mod_wsgi` to serve Python apps, and helper package `python-setuptools`
10. Resolved warning message `Could not reliably determine the servers's fully qualified domain name` after restart with `echo "ServerName HOSTNAME" | sudo tee /etc/apache2/conf-available/fqdn.conf`
11. Installed and configured `git` with my name and email
12. Installed additional packages to allow Flask application service: `libapache2-mod-wsgi` and `python-dev`
13. Enabled `mod-wsgi`
14. Created a test Flask App, installed Flask, enabled new Virtual Host, created .wsgi file [(Super helpful Digital Ocean tutorial)](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
15. Cloned GitHub repo and made .git directory not publically accessible via browser
16. Installed required modules for Item Catalog to run using `pip` [(Help with pip)](http://stackoverflow.com/questions/23901687/pip-install-broken-pkg-resources-find-distribution-returns-empty-list-in-req-py): `httplib2` [(Help with httplib2 install)](http://stackoverflow.com/questions/1882465/python-httplib2-module-not-found), `requests`, `oauth2` [(Help with oauth2 install)](http://chrisstrelioff.ws/sandbox/2014/07/02/install_oauth2_python_package_on_ubuntu_14_04.html), `sqlalchemy` [(Help with sqlalchemy install)](http://stackoverflow.com/questions/22353512/how-to-install-the-sqlalchemy-on-the-ubuntu), `python-psycopg2` 
17. Installed and configured PostgreSQL  [(This was vital because I kept needing to start over)](http://stackoverflow.com/questions/5408156/how-to-drop-a-postgresql-database-if-there-are-active-connections-to-it) [(This clarified syntax for editing original Item Catalog program)](http://docs.sqlalchemy.org/en/latest/core/engines.html ) [(Digital Ocean saves the day again)](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-14-04) [(And again)](https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps) [(And again!)](https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps)
18. Configure Oauth Settings [(This was handy with figuring out FB login)](http://stackoverflow.com/questions/37098718/client-oauth-settings-are-not-showing-in-my-app-advance-settings-in-facebook-log )