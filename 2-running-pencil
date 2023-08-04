Now let us run a simulation of streaming instability. We will use the a benchmark 2D run in a shearing box, unstratified, in the meridional plane 

On ceph

		cd ceph 

copy the sample 

		cp -rp $PENCIL_HOME/samples/2d-tests/streaming_instability/RunBA .

Enter the directory and let's modify the resolution 

		cd RunBA

A pencil code simulation has 5 configuration files that it needs to run a simulation. These are 

	src/Makefile.local
	src/cparam.local
	start.in
	run.in
	print.in

The src/Makefile.local chooses the modules to compiler. The src/cparam.local controls the resolution. start.in contains the initial conditions, run.in the run parameters, and print.in the diagnostic quantities to output to the time series. 

We will modify the resolution. Open src/cparam.local and edit the lines

		integer, parameter :: ncpus=16, nprocx=4, nprocy=1, nprocz=4
		integer, parameter :: nxgrid=256, nygrid=1, nzgrid=256
		integer, parameter :: npar=100000, mpar_loc=20000, npar_mig=100

		integer, parameter :: nbrickx=16, nbricky=1, nbrickz=16, nblockmax=128

And in `run.in`, let us change 

		nt = 10000000, it1 = 25
		lpencil_check=F
		itorder = 3

Finally         
                
		pc_setupsrc

This will populate the `src/` directory with soft links. Now do 

		pc_build
 
this command will compile the code and produce the `*.x` executables in the `src/` directory. Once the compilation is done, create a data directory 

		pc_mkdatadir

Which is a shortcut pencil command for creating a data directory. In this case, it will simply creat a hardlink data/ subdirectory (in other clusters you may want to configure pc_mkdatadir to generate a softlink data/ subdirectory, linked to the /scratch or /work level of the cluster).

