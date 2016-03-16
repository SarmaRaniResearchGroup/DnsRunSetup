# Setting up just fluid part
+ **Changes to be made to makefile**  
Comment out the DPARTICLE option AND keep DFORCING option if you need stochastic forcing.  
+ **Changes to be made to parameters file**  
Change or set Isodecay to desired value.  
Change dt (dt decreases as N increases).  
Change nu (nu decreases as N increases).  
Change itime_min (if restarting the run).  
Change Stats_time and Spec_time if you want to collect stats and write spectrum
at a different interval.  
+ **Changes to be made in driver.f90 file**  
Use pulse_start_corr to start or initialize a new velocity field.  
Comment out the restart file calls: 'call startsmall or startbig'.  

# Restarting the fluid part  
comment out 'call pulse_start_corr' and uncomment restart file calls: 'call startsmall or startbig'.  

# Introducing particles after fluid flow-field achieved stationarity  
+ **Changes to be made to makefile**  
Uncomment the DPARTICLE option.  
Add DTRACK option if you want particle tracking.  
+ **Changes to be made to parameters file**  
Change itime_min = IsoDecay in the fluid part.  
Change tau_eta to the averaged value obtained from Isostats.dat from the fluid part run.  
Change Isodecay to the desired value.  
Make sure that the initialization_flag = .true. and restart_flag = .false.  
Change file_flag = .true., if you want to write out S^2 and R^2 data.  
Change thresh_time and end_tr_time if particle tracking is on.  

+ **Changes to be made to the run directory**  
Make sure the directories required for tracking particles are present.

+ **Changes to be made to pardata_new.dat file**  
Make sure the desired number of St are listed and value in the second column = NDSIP/StClass in global.f90.  
+ **Changes to be made to driver.f90 file**  
Comment out the 'call pulse_start_corr'.  
Uncomment the restart files calls: 'call startbig or startsmall'.  
Also, check the timestep after which you're writing particle stats and .tgz files. 

# Restarting with particles  
+ **Changes to be made to parameters file**  
Change itime_min equal to the time step you want to restart from + 1 (+1 because in the 
code itime=itime_min - 1. Therefore, restart files read will be corresponding to the itime_min - 1).  
Change IsoDecay if required.  
Change restart_flag = .true.  
Change initialization_flag = .false.  
+ **Things to check in driver.f90**  
Make sure the path of directories for particles locations (parpos), number of particles (parlog) and particles  
velocities (accel) is correct. Also, the parpos and accel files at the restart time should be present in these 
directories.
