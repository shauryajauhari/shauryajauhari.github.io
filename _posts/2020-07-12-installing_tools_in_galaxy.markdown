---
layout: post
title: Installing Tools in Galaxy
date: 2020-07-12 13:06:19 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: galaxyProject.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Galaxy]
---


<p> Ton install tools into a local installation (development version) of galaxy, we may refer this <a href = "https://galaxyproject.org/admin/tools/add-tool-from-toolshed-tutorial/" > link</a>, methodology for which has been briefly described below.</p> Tools can be installed into galaxy using <i> Tool Shed</i>, and several other options that also allow to incorporate custom tools. However, for the limited scope of this tutorial, we shall stick to installing tools with <b>Tool Shed</b>. 

## Tool Shed
<p> As the name suggests, this could be deemed as a master-repository that holds other repositories with certain standard set of tools, that a typical galaxy environment would require; an suitable analogy to tool shed could be <a href = "https://cran.r-project.org/" > CRAN </a> in R that holds various packages for distinct usages. Since the development version of galaxy, that a user installs, is a <i>virgin</i> instance, we need to load it up with the kind of tools pertinent to our analysis. The protocol is listed as below.</p>
<br>

<ol>
<b> <li> Connecting to Tool Shed </li></b>
<p> By default, galaxy is already connected to the <a href = "https://toolshed.g2.bx.psu.edu/" > Main Tool Shed </a>. Another requisite to install tools from the tool shed, is <a href = "https://www.mercurial-scm.org/" > Mercurial </a> that must exists in the system hosting the developmental version of galaxy. 
To ensure that the galaxy is connected to the main tool shed, view the configuration file for galaxy. </p>

<p align="left">
  <img width="400" src="/assets/img/cmdConfigGalaxy.png">
</p>

<p>The following entry is the link to the resource. Likewise, any number of tool sheds could be appended to the galaxy instance.</p>

<p align="left">
  <img width="600" src="/assets/img/xmlToolShed.png">
</p>
<br>

<b><li> Open the Tool Shed </li></b>

<p>In the galaxy interface, go the the admin control tab.</p>
<p align="left">
  <img width="400" src="/assets/img/gotoAdmin.png">
</p>

<p>Select "Install and Uninstall" option under the "Tool Management" section on the left.</p>

<p align="left">
  <img width="600" src="/assets/img/installToolsGalaxy.png">
</p>
<br>

<b><li> Installation </li></b>

<p> For example, let us try installing <i>fastqc</i> into the system. </p>

<p>In the "search repositories" text input control, search for the keywork "FASTQC".</p>
<p align="left">
  <img width="400" src="/assets/img/selectTool.png">
</p>

<p>We'll notice several instances of the tool. Preferentially, we'll select the most popular one.</p>

<p align="left">
  <img width="600" src="/assets/img/fastqc.png">
</p>
<br>

<p> On selecting the tool, a confirmation window appears. </p>

<p align="left">
  <img width="600" src="/assets/img/clickOkay.png">
</p>
<br>

<p> We can also choose to view the <i>Advance Settings</i> that provide options to install dependencies for the selected tool.</p>

<p align="left">
  <img width="600" src="/assets/img/advancedSettings.png">
</p>
<br>

<p> Finally, the tool gets cloned and installed in the galaxy. </p>

<p align="left">
  <img width="600" src="/assets/img/inProgress.png">
</p>
<br>

<p align="left">
  <img width="600" src="/assets/img/toolDone.png">
</p>
<br>

</ol>