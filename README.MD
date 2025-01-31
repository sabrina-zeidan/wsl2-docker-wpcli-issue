## **My heart’s desire:** 
access WP-CLI functions in WordPress docker in Ubuntu 
<br /> 
### Environment: 
Windows 10 Home with Hyper-V enabled; WSL2; Docker Desktop with WSL2 support enabled; Ubuntu 20.04
<br /> 
### To achieve this (as far as my understanding):
* WP and WPCLI should be sharing the same volume, and the same network
* I need to pass the same variables to WPCLI as to WP (changes from March 2021 [here](https://hub.docker.com/_/wordpress)) 
* The IP address that WSL uses changes whenever the computer is restarted. 
* Ubuntu user has to be specified for WPCLI, www-data for WP and www-data user for WPCLI have different ids [https://www.buzzphp.com/posts/how-to-run-wp-cli-in-docker-composeyml](https://www.buzzphp.com/posts/how-to-run-wp-cli-in-docker-composeyml)   
### Result so far:
![unnamed](https://user-images.githubusercontent.com/5646904/132088875-1847fec1-cf75-4260-bf3a-1c5883b644d2.png)
$ docker-compose up -d 

Then in WP root:

$ wp user list

**Error: This does not seem to be a WordPress installation.**

 I was not able to pass the path recognized properly as well (see below).
<br /> 
<br /> 
_I tried 2 ways to achieve this, both are getting me closer but still not there._
<br /> 
<br /> 
### Way #1 not named volumes, WP installation in the directory where docker-compose.yml is located

docker-compose.yml for this  https://github.com/sabrina-zeidan/wsl2-docker-wpcli-issue/blob/main/docker-compose-not-named-volumes.yml

**Why it doesn’t work:**

I believe that not named volumes, though having the same location don’t get bundled together, so WPCLI has no idea there is WP there.
<br />
<br /> 
### Way #2: named volumes, WP installation god knows where

docker-compose.yml for this: https://github.com/sabrina-zeidan/wsl2-docker-wpcli-issue/blob/main/docker-compose-named-volumes.yml
 
**Why it doesn’t work:**

This seems like it should work in the end. The problem I encountered here is that** I just can’t navigate to WP installation folder in Ubuntu.**

In WSL2 containers are not accessible from ubuntu by default, they can be located in Windows but not in Ubuntu \
This worked for me: [https://github.com/microsoft/WSL/discussions/4176#discussioncomment-831817](https://github.com/microsoft/WSL/discussions/4176#discussioncomment-831817)   \
But just once, after PC restart it doesn’t work anymore, I tried the last answer in that thread — didn’t make a trick.
This is related https://github.com/microsoft/WSL/issues/3854#issuecomment-631356968

This MySQL sleep thing worked for me! But just one time as well. 

[https://question-it.com/questions/3371307/kak-zapustit-wp-cli-v-docker-composeyml](https://question-it.com/questions/3371307/kak-zapustit-wp-cli-v-docker-composeyml) 

UPD: about making WSL2 communicate with Windows installs https://anchor.host/local-lightning-and-upgrading-to-wsl2/

