Now let us visualize the results. Let's read the time series and plot the maximum dust density vs time. For that, you need to ssh into rusty via "ssh -Y rusty" after getting on the login

```
import matplotlib
matplotlib.use('TkAgg')
import matplotlib.pyplot as plt
import pencil as pc
import numpy as np

ts=pc.read.ts()
plt.plot(ts.t/2/np.pi,ts.rhopmax)

plt.xlabel(r'$t/T_0$')
plt.ylabel(r'max($\rho_p$)/$\rho_0$')
plt.yscale('log')
plt.title("Maximum Dust Density vs Time")
plt.show()
```

This should be the result. The abscissa is in orbital periods, the ordinate is maximum dust normalized by the reference gas density. 

<img src="maxdust.png" alt="maxdust" width="400"/>

Now let us inspect the a contour plot of the dust density. 

```
import matplotlib
matplotlib.use('TkAgg')
import matplotlib.pyplot as plt
import pencil as pc
import numpy as np

ff=pc.read.var(trimall=True)
rhop = ff.rhop[:,0,:]
amax = np.log10(rhop.max())
amin = amax - 4
rmin=10**amin
i = np.where(rhop < rmin) 
rhop[i] = rmin
plt.contourf(ff.x,ff.z,np.log10(rhop),np.linspace(amin,amax,256),cmap='inferno')

plt.xlabel(r'$x$')
plt.ylabel(r'$z$')
plt.colorbar(label=r"$\log_{\rm 10}(\rho_p/\rho_0)$")
plt.title("Streaming Instability")
plt.show()
```

<img src="streaming.png" alt="streaming.png" width="400"/>
