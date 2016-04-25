# Stash 3.11.6 to Bitbucket 4.5.2

[Complete Steps](#completesteps)

![Stash Logo](https://blog.seibert-media.com/wp-content/uploads/2015/12/Stash-Artikelbild.png)
![Bitbucket Logo](https://wac-cdn.atlassian.com/dam/jcr:e2a6f06f-b3d5-4002-aed3-73539c56a2eb/bitbucket_rgb_blue.png?cdnVersion=8)

<a name="completesteps">
##Complete Steps:
</a>

* **Upgrade/Update to Java 8**
	* Use jenkins-alfred-base/recipes/java8.rb for help
	* Change chef to alter the stash bash profile script, 'set-java-home.sh' to correctly set the home for Java 8.
	* Set the java home manually (if above step not complete)
	
* **Do a complete backup of the current server**

* **Download bitbucket server 4.5.2**
	* ```wget https://www.atlassian.com/software/bitbucket/download```
	* ```mv tarball to /mnt/stash/atlassian```
	* chown stash:stash atlassian-bitbucket tar file
	
* **Stop chef-client**
	* ```service chef-client stop```
	
* **Become the stash user**
	* ```su stash```
	
* **Untar the tar ball in /mnt/stash/atlassian**

* **stop the current stash 3.11.6**
	* ```service stash stop```
	
* **Change the /etc/init.d/stash file**
	* Change STASH_INSTALLDIR
	* Replace instances of Stash with bitbucket
		* ```:%s/Stash/bitbucket/```
		
* **Check files in /mnt/atlassian/application-data/stash/shared**
	* Find server.xml
		* If not there, re-run chef-client to generate server.xml
			* Make sure to re-change /etc/init.d/stash if you re-run chef-client
		* Change all instances of stash in names/filepaths to bitbucket
			* only necessary because updating from stash to bitbucket
			
* **Check setenv.sh, see if it's different/been changed on the main server**
	* If so, copy the changes
	
* **Double check to make sure the old stash is stopped**
	* run stop-stash.sh in old stash folder if needed
	
* **Start the new bitbucket server**
	* ```service bitbucket start```
	
* **Check everything is running fine and it displays the correct version number**

* **Finally, update all plug-ins and check they are working in gui**



