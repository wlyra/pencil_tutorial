Now let us visualize the results. Let's read the time series and plot the maximum dust density vs time 

		import pencil as pc
		import pylab as plt 
		import numpy as np

		ts=pc.read.ts()
		plt.plot(ts.t/2/np.pi,ts.rhopmax)

		plt.xlabel(r'$t/T_0$')
		plt.ylabel(r'max($\rho_p$)/$\rho_0$')
		plt.yscale('log')
		plt.title("Maximum Dust Density vs Time")
		plt.savefig("maxdust.png")

<img src="maxdust.jpg" alt="maxdust" width="200"/>
