

## Setting up your rusty environment for Pencil

Obtain the pencil code by git cloning into your home directory

	git clone https://github.com/pencil-code/pencil-code.git

Next go to the pencil-code directory, and execute the sourceme.sh 

	cd ~/pencil-code
	source sourceme.sh

Next add these lines to your ~/.bash_profile

	export PENCIL_HOME=~/pencil-code
	export PENCIL_CONFIG_FILES=$PENCIL_HOME/config/hosts/rusty/rusty.conf
	PATH=$PENCIL_HOME/bin:$PENCIL_HOME/utils:"${PATH}"
	module load openmpi

