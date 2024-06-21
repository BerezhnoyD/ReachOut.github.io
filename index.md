---
title: Home
layout: home
---
# Testing the new website hosting the documentation for the ReachOut project
# ReachOut platform
[![DOI](https://zenodo.org/badge/517810120.svg)](https://zenodo.org/doi/10.5281/zenodo.7383917)

### Background
Did you know that mice are pretty good at using their forepaws? See for yourself...
![Image]({{ site.baseurl }}/images/reachout.gif)  
Reach-to-grasp task in rodents first developed by Ian Whishaw 'Whishaw et al., 1990' has recently became the gold standard for the study of fine motor behavior in rodents. The structure of the movement and the neurocircuitry behind it can be well translated between rodents and higher primates including humans which makes this task very popular for the study of cortical motor control. We see an increasing use of reach-to-grasp task along with development of apparatuses for this task that could be used together with current neurophysiological tools like 2-photon imaging for the study of neural activity during execution of the planned motor command. However, there are not many designs available for the reach-to-grasp task in freely behaving mice. 
With the dawn of DIY electronic kits (Arduino) and stereolithography 3D printer technology we see the field of open-source behavioral box design rapidly expanding and even being a major driver of neuroscience discoveries. There are multiple designs for Skinner boxes and rodent operant chambers proposed by different laboratories. However, there are fewer solutions to study fine motor skills, probably due to the difficulties in precise presentation of the reinforcement and quantifying the kinematics of the small animal movements. The second problem has been recently solved with the use of deep-learning video analysis [DeepLabCut]. There are also several solutions for the automation of the classical reach-to-grasp task. The solutions specifically tailored for the behavior- neurophysiology coupling are usually made for head-fixed animals and focused on precise synchronization of the animal behavior, heavily constrained, with the neurophysiology recording. Training animals in such setups can be problematic and labor-intensive.  On the other side, apparatuses proposed to study reaching in freely behaving animals, following the line of operant boxes research, usually lack the precision and time resolution needed to synchronize with external devices used in neurophysiology research. Moreover, research with automatic learning boxes generally focus on simple metrics like the number of trials and success rate of reaching and overlook more sophisticated kinematic analysis which requires better video quality, precision and post-processing of the behavioral data. Thus, there is always a tight balance between the open-source (ease of manufacture) and temporal precision needed for neurophysiology and precise kinematic studies.  Trying to fill this gap we implemented a DIY system for mice, using the current state-of-the-art solutions in 3D printing and data analysis and made it accessible to the large open-science community.



### Overview of the project
The following project describes the design, fabrication, assembly and use case of the open-source hardware platform
for mice reach-to-grasp task training and fine motor skill video analysis. We present the behavioral platform - 
automated mouse Reaching Box that was designed to be 3D printed and hence easily reproducible. 
The device is used to train animals to perform reach-to-grasp dexterity task: approach the proximal part of the reaching box
and reach for single sugar pellets disposed by motorized feeder disk located in front of the narrow slit. 
This task is used for studying planning and execution of fine motor skills requiring cortical control of the forepaw and finger movement. 
Behavioral platform allows to record the video and track the forepaw and fingers during the reaching movement. 
This tracking data (performed by DLC networks) can be analyzed further to extract different kinematic parameters 
(speed, acceleration, jerk, accuracy) and different moments of the reach (start, peak, end) 
to use them as behavioral keypoints (ex. peri-event analysis).

Hardware used in the design of the platform, aside from the high-speed FLIR camera, 
consists of readily available open-source components that can be acquired relatively 
cheap or fabricated with the use of stereolithography 3D printer. Software is written in Python and organized in multiple Jupyter Notebooks.

### Hardware overview
![alt text]({{ site.baseurl }}/images/Slide2.PNG)
All the schematics, 3D models and assembly instructions are provided in this repository. The assembled box is programmed with Arduino IDE for its use as a standalone device for automated/semi-automated animal training and behavioral data acquisition. The reaching box can log basic behavioral data (touch/beam sensors) and is designed to be connected to external devices to trigger in vivo imaging, optogenetic stimulation etc. It can stream the synchro signal from the behavioral events recorded by the onboard sensors with millisecond resolution, which makes it ideally fitted for synchronized behavioral-neurophysiology experiments. With the use of multiple mirrors, the system can acquire multiple close-up views for 3d trajectory reconstruction (triangulation) of the reach-to-grasp movement with a single high-speed FLIR camera when connected to the desktop PC. The output of the system is a behavioral video of the reaching movements throughout the learning session along with the tsv table of the synchronized data from Arduino.

### Software overview
![alt text]({{ site.baseurl }}/images/Slide3.PNG)
In addition to the hardware part, we provide the complementary software data analysis pipeline which can be performed off-line with the acquired videos. Python package for the 3d trajectory reconstruction and kinematic analysis is organized in classes and modules implemented in a series of Jupyter Notebooks and based on the state-of-the-art solutions for the markerless pose estimation as well as original code
 - [DeepLabCut] is used for intial tracking using pretrained ResNet architecture (& training it). 
 - [Anipose Lib] is used for the 3d triangulation part to restore the action in absolute coordinates (mm).
 - [ReachOut] is our humble code contribution and is used for all the analysis on kinematic traces.
 
The [ReachOut] pipeline guides user through the number of steps to extract the parts from the video, track and triangulate the points of interest (paw, fingers), cluster the reaches, visualize and compare basic kinematic parameters for different reaching categories. User has the ability to export the final data on the kinematics (scalars for each reach) and reaching timestamps as a *.h5/.csv table for further analysis or synchronization with his own pipeline.


The repository contains all the materials to build the mouse reaching task and analyze the data acquired with this task
- Bill of materials to build the reaching box
- 3D models for the components of the box
- Schematics for the reaching box Arduino-based controller
- Scripts to run the video recording from the FLIR Camera and logging the data from Arduino
- Scripts for the full analysis dataflow: detecting body parts with DLC and getting the reaching trajectories

## Installation
### Recording toolbox
The recording toolbox contains two parts: 
- one on the Arduino side (script should be uploaded to the microcontroller with the use of Arduino IDE)
- and one on the PC side. This one is just the snippet to record from the FLIR camera and simultaneously record from Arduino.
The second part is taken with minor changes from the PySpin repository, so you should follow the installation instructions listed there
(https://github.com/neurojak/pySpinCapture)


### Analysis toolbox
The analysis toolbox is dependent on certain python libraries and programs (DEEPLABCUT, ANIPOSE) and Jupyter Notebook.
DEEPLABCUT (https://github.com/DeepLabCut/DeepLabCut)
ANIPOSE (https://github.com/lambdaloop/anipose)

To make it easier for installation all the dependencies are included in the updated *DEEPLABCUT.yml conda environment file.




# Sorry for this part, it is still from Just-the-Docs template and used for testing

This is a *bare-minimum* template to create a Jekyll site that uses the [Just the Docs] theme. You can easily set the created site to be published on [GitHub Pages] – the [README] file explains how to do that, along with other details.

If [Jekyll] is installed on your computer, you can also build and preview the created site *locally*. This lets you test changes before committing them, and avoids waiting for GitHub Pages.[^1] And you will be able to deploy your local build to a different platform than GitHub Pages.

More specifically, the created site:

- uses a gem-based approach, i.e. uses a `Gemfile` and loads the `just-the-docs` gem
- uses the [GitHub Pages / Actions workflow] to build and publish the site on GitHub Pages

Other than that, you're free to customize sites that you create with this template, however you like. You can easily change the versions of `just-the-docs` and Jekyll it uses, as well as adding further plugins.

[Browse our documentation][Just the Docs] to learn more about how to use this theme.

To get started with creating a site, simply:

1. click "[use this template]" to create a GitHub repository
2. go to Settings > Pages > Build and deployment > Source, and select GitHub Actions

If you want to maintain your docs in the `docs` directory of an existing project repo, see [Hosting your docs from an existing project repo](https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md#hosting-your-docs-from-an-existing-project-repo) in the template README.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[DeepLabCut]: https://github.com/DeepLabCut/DeepLabCut/
[Anipose Lib]: https://github.com/lambdaloop/aniposelib/
[ReachOut]: https://github.com/BerezhnoyD/Reaching_Task_VAI/
[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[GitHub Pages]: https://docs.github.com/en/pages
[README]: https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md
[Jekyll]: https://jekyllrb.com
[GitHub Pages / Actions workflow]: https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/
[use this template]: https://github.com/just-the-docs/just-the-docs-template/generate
