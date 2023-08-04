
Now let's make a video. On the run directory, type 

		pc_build -t read_all_videofiles
		src/read_all_videofiles.x 
        
That will compile the video reader, and combine the slices output by each processor. 

Run now the following script. 

```
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import math
import pencil_ccy as pc
import os

istride = 10

path = "videos"
exists = os.path.exists(path)
if not exists:
    os.mkdir(path)

##################################################                                                    

# Get grid, common data                                                                               

g = pc.read.grid()
x = g.x
z = g.z

xmin = math.floor(x[0])
xmax = math.ceil(x[-1])
zmin = math.floor(z[0])
zmax = math.ceil(z[-1])

t, s = pc.read.slices("rhop")
rhopxz = np.log10(s.xz)

# Range of gas density color bar                                                                      
linmin = -2
linmax =  2

# Plotting                                                                                            

tshape,xshape,yshape=rhopxz.shape

for i in np.arange(0,len(t),istride):

    plt.figure(figsize=(2*3.6,2*1.5*2.7))
    ax = plt.gca()
    ax.set_aspect('equal')
    ax.set_ylabel(r"$y$")
    ax.set_xlabel(r"$x$")
    ax.set_xlim(xmin,xmax)
    ax.set_ylim(zmin,zmax)

    # Choose timeindex of plot                                                                        
    rhoi = rhopxz[i,:,:]
    j = np.where(rhoi < linmin) 
    rhoi[j] = linmin
    im=plt.imshow(rhoi.T,extent=(min(x),max(x),min(z),max(z)),vmin=linmin,vmax=linmax,cmap='inferno')
    print(f"Saving videos/{i:05}.png")
    plt.savefig(f"videos/{i:05}.png",bbox_inches="tight")
    plt.close()

```

navigate to the video folder and do 

		ffmpeg -framerate 16 -pattern_type glob -i '*.png' -c:v libx264 -vf "fps=16,format=yuv420p,pad=ceil(iw/2)*2:ceil(ih/2)*2" movie.mp4
