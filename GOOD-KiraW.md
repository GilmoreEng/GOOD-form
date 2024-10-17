# GOOD 1:1 Meeting 
Name: Richard Gilmore & Kira Wells
Date: 10-11-2024
## Goals/Projects/Items of Interest 
|Topic|Update|
|:---:|:---:|
|Expand SciViz offering, workshop, and awareness| No response from Sebnem. Draft propsoal description for CIO - draft and research of links for example to send.
|OmniGlobe CoorsTek| Owner Physics DH: Frederic Sarazin. Email chain with vendor: Adam Wales, email: adam@elumenati.com. Meet with Sonja Mayotte, POSTDOCTORAL FELLOW, DEPARTMENT OF PHYSICS, and Eric Mayotte didn't come. Quick explaination of system and set follow up meeting in-person to go over maintenance and software operations.
|Website content| https://cu-boulder-crdds.github.io/LearningMaterials/PythonDataViz.html. 
|Test Visualization Software Workflows for Collaboration| Need to reinstall with Entitlement and Enterprise version. Need code and architecture plan, code deployment, etc. Genaric email instructions recieved.
|Ease-of-use access to HPC at Mines through improvements to Open Ondemand| Fix up JupyterLab Deployment, Document all changes in logs, copy code to github RC repo. Fix python envs in jupyterLab. Deploy MINES OOD apps at gibhub. Debugging Ruby code for YAML parsing of repeative code on MIO juypter app to start.
|Fall Student Project | Github repo: https://github.com/TriHardStudios/F23_CSM_Gilmore. Need to integrate CS OOD Apps into new version.
|Personal Development| "Unity Teaching BETA trainning:" Voucher recieved. Need to find the materials to review, and then schedule exam at Arvada RRCC testing center. HR training review of Accountability and Teamwork sessions.
|Culture/Community| Revised documentation workflow into gitlab and sphinx. Copy and corrected "procedures" tree.
|TDX/Service|
|On-prem Cluster| Handled Wendian storage filling up above 90% stopping more jobs from starting becuase of Node Health Check (nhc). Changed limit to 94% in /etc/nhc/nhc.conf and pushed out to nodes using 'nodeupdate slurm -F' and xdsh compute,gpu 'nhc' to clear nhc on drained nodes. Found user filling up the disk with a job "Ahmad Tourei" using 232T from a single 33-node job.
|Cloud/HPC IaaS| 
|Admin Automation App|
|Apps| Update OOD to new version of python module. Not pushed yet. Matlab 2024a rewrite html server app.
|Build CloudCompare| Uses FLATPAK manager in Q2.
|Vis&GUI| Look into v3.1 "my projects" which replaces "my templates".  Test Mark III sys workshop material, Nick never tested it.
|Website| Website Docs out of date need to update after workshop. See above. Also update SciVis offering. Need access to WPFILES for rc.
|BIZ model discussion| completed 150-175 and updated pie charts. Scaled study from top 10,50,100,150,200 for trends. Need to review Governance drafted by Kira.
## Obstacles
|Identify roadblocks in the way of goal/project completion and overall employee success.|
|---|
|Need team to test code I send them.|
## Opportunities 
|Discuss new opportunities for further learning, development, and growth.|Comments|
|:---:|:---:|
|NVIDIA DLI| Testing on Wendian, needed to fix JupyterLab envs first, ready to try again. Give it shot on building it on DELTA.~
|GRANT: Eng. a Trajectory of Success| Workshop set for January. Sent USD file edits to team. Waiting feedback.
|Andy discussion at Markiiisys| Have a thing to push for money. Design a thing. Perhaps use Edgar Vis-lab. Veronica Allyson, ME explosive prof., And use it for education. Value model for safety.  
|FSAE team meeting| Met with Connor Wilde and Jack Betz. Decided on getting students on both Mio and Wendian student partition. They are teaching CFD to the incoming freshman one hour a week on Monday. Gave access to ANSYS installers on Orebits3.
## Decisions
###Agreed upon actions to be taken.
|Topic|Decision|
|:---:|:---:|
|Python session ideas|  What's the journey from 2D to 3D data and beyond
|Data Center capacity?|What is the power and cooling? 