# GOOD 1:1 Meeting 
Name: Richard Gilmore & Kira Wells
Date: 1-9-2025

## Goals/Projects/Items of Interest 
|Topic|Update|
|:---:|:---:|
|Expand SciViz offering, workshop, and awareness| Library "Data Visualization" workshop session scheduled for March 5th.
|OmniGlobe CoorsTek| Need to review content management system to maintain functional content on globe.
|Website content| https://cu-boulder-crdds.github.io/LearningMaterials/PythonDataViz.html. 
|Test Visualization Software Workflows for Collaboration| Test omniverse nucleus-dev.mines.edu data management and connection complete! SSL certificate installed. Username and password management currently is a manual process. Tested Unity plugin to LIVE connection started from Omniverse SKD Kit, and USD composer app. MACOS fails to be useful and can't run connectors in unity. Unity 6 is export and import only. 2023 Unity has Live Beta working. Recorded video of 2023.
|Ease-of-use access to HPC at Mines through improvements to Open Ondemand| Fix up JupyterLab Deployment, Document all changes in logs, copy code to github RC repo. Fix python envs in jupyterLab. Deploy MINES OOD apps at gibhub. Debugging Ruby code for YAML parsing of repeative code on MIO juypter app to start. Functional VNC and matlab-proxy need to cleanup code. Fixed AGEDU app. Put in RFC for change after meeting with Team to review each change.
|Fall Student Project | Github repo: https://github.com/TriHardStudios/F23_CSM_Gilmore. Need to integrate CS OOD Apps into new version.
|Personal Development| "Unity Teaching BETA trainning:" Voucher recieved. Need to find the materials to review, and then schedule exam at Arvada RRCC testing center. Complete Group Fitness Instructor (GFI). Need to study questions and get CPR certified.
|Culture/Community|
|TDX/Service| Testing of ParaView server setups and job templates for easy launch in OOD. build paraview reader macro, and ask for better method to test. Jupyter Lab launch issue was from Josh saturating network and slowing down /sw stalling Jupyter server startup. Installed VMD binary for Swarup Banerjee. Emailed Luis about GCP pilot.
|On-prem Cluster| Mio is still command-line only.
|Cloud/HPC IaaS| 
|Admin Automation App|
|Apps| Fix VMD launch code to use "xfce4-terminal --command=`which vmd`" and removed #--sm-client-disable flag to recover windowing controls for user interface. Need to correct this behavior in other apps. Sent RFC.
|Build CloudCompare| Discuss with Team about deployment method with Flatpak -- 1/3/2025. Nick will attempt to build from source. Flatpak is a bit like conda, and can balloon user home directories. Further discussion on 20GB limit to come.
|Vis&GUI| Look into v3.1 "my projects" which replaces "my templates".  Need test Mark III sys next notebooks and download datasets. Ready to release new version of JupyterLab and python 2024 as the base environment for OOD app.
|Website| Completed publication of website pages and added prime 2d plots.
|BIZ model discussion|
## Obstacles
|Identify roadblocks in the way of goal/project completion and overall employee success.|
|---|
|copying Z drive files to OneDrive| ticket open, ticket passed to 365 support. No response. Day spent figuring out appropriate tool native to Windows. Verification of copied data and resolution of conflits.
## Opportunities 
|Discuss new opportunities for further learning, development, and growth.|Comments|
|:---:|:---:|
|NVIDIA DLI| Testing on Wendian, needed to fix JupyterLab envs first, ready to try again. Give it shot on building it on DELTA.~
|GRANT: Eng. a Trajectory of Success| Group workshop meeting on Jan 9-10 at Golden hotel. 
## Decisions
###Agreed upon actions to be taken.
|Topic|Decision|
|:---:|:---:|
|Cureate list useful tutorials | Data clean up tools, aka panads and holoviews, or Amazon Sagemaker. Need to be able to see dirty data to make judgement calls on clean up. Identify easy cleanup such as bad sensor data, static, and Not-a-Number. https://pointclouds.org/ is C++ PCL library with tutorials. Also see: https://robotica.unileon.es/index.php?title=PCL/OpenNI_tutorial_2:_Cloud_processing_(basic) or ROS: https://wiki.ros.org/pcl/Tutorials. 