

## Setting up your rusty environment for Pencil

Obtain the pencil code by git cloning into your home directory on rusty

		git clone https://github.com/pencil-code/pencil-code.git

Next go to the pencil-code directory, and execute the sourceme.sh 

		cd ~/pencil-code
		source sourceme.sh

Next add these lines to your ~/.bash_profile

		export PENCIL_HOME=~/pencil-code
		export PENCIL_CONFIG_FILES=$PENCIL_HOME/config/hosts/rusty/rusty.conf
		PATH=$PENCIL_HOME/bin:$PENCIL_HOME/utils:"${PATH}"
		module load openmpi

And source it. You should be ready to compile the code. Let's make sure that everything is ok by compiling a test serial run. Jump to 

		cd $PENCIL_HOME/samples/2d-tests/globaldisc/

We will run an `pc_auto-test`. Auto-test is a pencil command that checks if a run is giving the same results as a reference file. It is also useful to catch compilation errors. This pencil command resides in `pencil-code/bin`. You have this in your `$PATH`, so it should find it. Type

		pc_auto-test -C .

(Do not forget the dot!)

The -C is for cleaning leftover files from previous compilations. The dot says that you want to auto-test the current directory.  

You should see 

	[me@rusty globaldisc]$ pc_auto-test -C . 
	
	/mnt/home/me/pencil-code/samples/2d-tests/globaldisc:
	    Compiling..                               ok      
	    Starting..                                ok      
	    Running..                                 ok      
	    Validating results..                      ok      
	
	----------------------------------------------------------------------
	Test succeeded.
	
	----------------------------------------------------------------------





Do not forget the dot! 