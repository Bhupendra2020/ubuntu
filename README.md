fnubhupen-ubuntu
============

Simple Ubuntu docker images with SSH access


Usage
-----

To create the image `fnubhupen/ubuntu` with one tag per Ubuntu release, 
execute the following commands on the fnubhupen-ubuntu branch:
	
	docker build -t fnubhupen/ubuntu:latest .
	
	docker build -t fnubhupen/ubuntu:lucid lucid/
	
	docker build -t fnubhupen/ubuntu:precise precise/
	
	docker build -t fnubhupen/ubuntu:quantal quantal/
	
	docker build -t fnubhupen/ubuntu:raring raring/
	
	docker build -t fnubhupen/ubuntu:saucy saucy/
	
	docker build -t fnubhupen/ubuntu:trusty trusty/


Running fnubhupen/ubuntu
--------------------

To run a container from the image you created earlier with the `trusty` tag 
binding it to port 2222 in all interfaces, execute:

	docker run -d -p 0.0.0.0:2222:22 fnubhupen/ubuntu:trusty

The first time that you run your container, a random password will be generated
for user `root`. To get the password, check the logs of the container by running:

	docker logs <CONTAINER_ID>

You will see an output like the following:

	========================================================================
	You can now connect to this Ubuntu container via SSH using:

	    ssh -p <port> root@<host>
	and enter the root password 'U0iSGVUCr7W3' when prompted

	Please remember to change the above password as soon as possible!
	========================================================================

In this case, `U0iSGVUCr7W3` is the password allocated to the `root` user.

Done!


Setting a specific password for the root account
------------------------------------------------

If you want to use a preset password instead of a random generated one, you can
set the environment variable `ROOT_PASS` to your specific password when running the container:

	docker run -d -p 2222:22 -e ROOT_PASS="mypass" fnubhupen/ubuntu:trusty


Adding authorized keys
----------------------

If you want to use ssh key for login, you can use `AUTHORIZED_KEYS` environment variable. The public keys are separated by `,`:

    docker run -d -p 2222:22 AUTHORIZED_KEYS="pubkey1, pubkey2, pubkey3" fnubhupen/ubunut:trusty

If you put the corresponding private key under `~/.ssh/` where you run ssh command, you will not be asked to input the password.

