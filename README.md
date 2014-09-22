svn-to-git
========

Docker : CentOS6 and base infrastructure for svn to git conversion

## Yo

1. create image from Dockerfile

		$ docker pull yukinagae/svn-to-git

2. start container from image
	
		$ docker run -it -p 80:80 yukinagae/svn-to-git /bin/bash

## SVN to Git (in the container)

1. extract author info

		# java -jar /usr/local/src/svn-migration-scripts.jar authors [svn repo url] [username] [password] > /usr/local/src/authors.txt

2. edit author info

		# vi authors.txt
		-> replace dummy email addresses to proper ones

3. convert to git

		# git svn clone --stdlayout --authors-file=/usr/local/src/authors.txt [username] [password] /usr/local/src/[repo name]


** choose 4-A or 4-B which you want !! **

4-A. zip git folder and download from browser

		# zip -r /var/www/html/[repo name].zip /usr/local/src/[repo name]
		-> now you can download zip folder from http://localhost/[repo name].zip

4-B. push git repository

		# cd /usr/local/src/[repo name]
		# git remote add origin [remote git url]
		# git push -u origin master
