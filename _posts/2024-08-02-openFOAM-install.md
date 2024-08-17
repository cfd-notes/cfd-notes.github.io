---
layout: distill
title: OpenFOAM-v2406 Installation
description: Installation of OpenFOAM-v2406 on Ubuntu 24.04 LTS and Windows 11.
tags: Install
categories: OpenFOAM
giscus_comments: false
date: 2024-08-02
featured: true

bibliography: 2024-08-02-openFOAM-install.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: WSL install on Win 11
  - name: OpenFOAM install on Ubuntu (via WSL)
---

## Introduction

In this post, I will go through OpenFOAM-v2406 installation process on Ubuntu 24.04 LTS and Windows 11.

First of all, what is OpenFOAM? OpenFOAM stands for Open Source Field Operation and Manipulation and it is free<d-footnote>You dont have to pay anything for OpenFOAM (free as a free beer), but mainly free in context of freedom. You can run the OpenFOAM as you want even for comercial purpose, you can change its code and redistribute it, you can even try to sell copies of OpenFOAM if you think that its good idea.</d-footnote> open source CFD software. Released under GNU General Public License. It contains pre-written collection of code in C++ that can be used to build solvers for computing a large spectrum of problems from continuum mechanics. Luckily, it also includes a set of tutorials that can be modified to suit our needs. Main focus is given to finite volume method (FVM) and fluid mechanics.

At the beginning, we will face the question of which version of OpenFOAM to begin with. Simply put, we have two main options. One is from OpenCFD Ltd, which is part of the ESI Group and whose distribution can be found at [openfoam.com](https://www.openfoam.com/). The other option is from the OpenFOAM Foundation at [openfoam.org](https://openfoam.org/).

Regarding this dilemma of which version of OpenFOAM to start with, a good summary can be found on the CFD-Online forum <d-cite key="OpenFOAM_Com_vs_Org2017"></d-cite>. From my personal perspective, I chose the version from ESI because it is used by people around me, so I opted for this option initially. However, in the future, it is definitely a good idea to try both distributions or even others and decide based on your preferences.

It is possible to immediately tell if the version of OpenFOAM is from ESI-OpenCFD ([openfoam.com](https://www.openfoam.com/)) or from the OpenFOAM Foundation ([openfoam.org](https://openfoam.org/)) because they use different versioning identifiers.

{% details Click here to know more about versioning differences %}

1. ESI-OpenCFD ([openfoam.com](https://www.openfoam.com/)) uses for OpenFOAM versioning a date-of-release identifier. The format is OpenFOAM-vYYMM, where:

   - YY represents the last two digits of the release year,
   - MM represents the month of the release.

   For example, OpenFOAM-v2406:

   - 24 indicates the year 2024,
   - 06 indicates the month of June.

   Previous release was OpenFOAM v2312. Every half year is expected new release distributed via [openfoam.com](https://www.openfoam.com/).

2. Foundation OpenFOAM ([openfoam.org](https://openfoam.org/)) uses for OpenFOAM versioning a sequence based identifier<d-cite key="OpenFOAM_org_version_history"></d-cite>. The format is OpenFOAM X.Y.Z, where:

   - X represents major version number,
   - Y represents minor version number,
   - Z represents patch version number.

   For example, OpenFOAM 2.3.1:

   - 2 indicates the major version number,
   - 3 indicates the minor version number,
   - 1 indicates the patch version number.

   Since the 2017 there are realised every year only major versions. For example current realise is from 9th July 2024 OpenFOAM 12, previous was OpenFOAM 11 realised in 11th July 2023.

{% enddetails %}

---

## WSL install on Win 11

One of the convenient ways to install OpenFOAM on Windows 11 is WSL (Windows Subsystem for Linux).

{% details Freshly installed Windows 11 %}
Edition Windows 11 Home\
Version 23H2\
Installed 31/07/2024\
OS build 22631.3880\
Experience Windows Feature Experience Pack 1000.22700.1020.0
{% enddetails %}

We are going to install everything needed for WSL using a PowerShell command, as suggested by the WSL documentation.<d-cite key="WSL_Doc"></d-cite>.

```powershell
wsl --install
```

This will, by default, install Ubuntu (in my case, Ubuntu 22.04.4 LTS). You will be asked to restart your system.

{% details Windows PowerShell -- WSL Installation %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-02-openFOAM-install/wsl_install.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

After restarting, a new window will pop up, and you will be asked to create a UNIX user account for Ubuntu. Your username should follow certain rules. For example, capital letters are not allowed. When you are typing your password, it is normal not to see what you are typing.

{% details After system restart -- Ubuntu set up %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-02-openFOAM-install/WSL_Ubuntu_default.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

And that's it. You have successfully installed Ubuntu. You can also install another GNU/Linux distribution. Already installed distributions can be listed with the command:

```powershell
wsl -l -v
```

and available distributions:

```powershell
wsl -l -o
```

The chosen distribution can be simply installed by specifying its name:

```powershell
wsl --install -d <Distro>
```

{% details Different GNU/Linux distributions %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-02-openFOAM-install/wsl_another_distro.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

You can then easily find your installed distribution in your Windows Apps.

{% details Inslatted GNU/Linux distributions in Windows Apps %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-02-openFOAM-install/Ubuntu_Search.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

---

## OpenFOAM install on Ubuntu (via WSL)

Now, we will finally install OpenFOAM. We can simply follow the quick-start steps from the OpenFOAM wiki for installing precompiled packages on Ubuntu.<d-cite key="OpenFOAM_wiki_install_Ubuntu"></d-cite>. So, in the Ubuntu terminal, we pass:

```bash
# Add the repository
curl https://dl.openfoam.com/add-debian-repo.sh | sudo bash

# Update the repository information
sudo apt-get update

# Install preferred package. Eg,
sudo apt-get install openfoam2406-default

# Use the openfoam shell session. Eg,
openfoam2406
```

Curl is used to download a file (script) from https://dl.openfoam.com/add-debian-repo.sh, and then it is 'passed' to bash for execution using pipe. This script adds the OpenFOAM repository to our Ubuntu system, so we can then simply update and install it. Running scripts from untrusted sources can be dangerous, and we should check what we are actually executing. Since sudo is used, you will be asked for your password.

{% details OpenFOAM Installation in WSL Ubuntu terminal%}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-02-openFOAM-install/OpenFOAM_Install.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

After running the apt-get install command, you will need to confirm that you want to continue by typing 'Y' when prompted. When it is finished, you can use OpenFOAM by:

```bash
openfoam2406
```

{% details OpenFOAM Installation in WSL Ubuntu terminal%}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-02-openFOAM-install/Installed_OpenFOAM.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

With that, we have successfully installed OpenFOAM-v2406.
