Now let us run a simulation of streaming instability. We will use the a benchmark 2D run in a shearing box, unstratified, in the meridional plane 

Navigate to the sample 

	cd $PENCIL_HOME/samples/2d-tests/streaming_instability/RunBA

and let's modify the resolution. A pencil code simulation has 5 configuration files that it needs to run a simulation. These are 

	src/Makefile.local
	src/cparam.local
	start.in
	run.in
	print.in

The `src/Makefile.local` chooses the modules to compile. The `src/cparam.local` controls the resolution. `start.in` contains the initial conditions, `run.in` the run parameters, and `print.in` the diagnostic quantities to output to the time series. 

We will first modify the modules, to run in a single processor. Open `src/Makefile.local` and edit the lines

	MPICOMM        = nompicomm
	PARTICLES       =   particles_dust
	#PARTICLES_MAP  =   particles_map_blocks 


Next, we'll modify the resolution. Open `src/cparam.local` and edit the lines

	integer, parameter :: ncpus=1, nprocx=1, nprocy=1, nprocz=1
	integer, parameter :: nxgrid=128, nygrid=1, nzgrid=128
	integer, parameter :: npar=40000

In `run.in`, let us change 

	nt = 10000000, it1 = 25
	lpencil_check=F
	itorder = 3
	dvid=0.05
	tmax=100.

Add also a `video.in` file to tell the code to output the particle density

	echo rhop > video.in

Finally         
                
	pc_setupsrc

This will populate the `src/` directory with soft links. Before
compiling, let's  add optimization so the code runs faster.
Add these lines to the end of `$PENCIL_HOME/config/compilers/GNU-GCC.conf`

	%section Makefile
		FFLAGS=-O3
	%endsection Makefile

Now do 

	pc_build
 
this command will compile the code and produce the `*.x` executables in the `src/` directory. The compilation should take about 5 minutes. (If you need to clean and build again, do `pc_build --cleanall`)

Once the compilation is done, create a data directory 

     mkdir data

Now start the run. 

	pc_start
	pc_run

The run should be fast, running one orbit every few minutes. The simulation will write output to the screen, and the same output yo the data/timeseries.dat filename. 
