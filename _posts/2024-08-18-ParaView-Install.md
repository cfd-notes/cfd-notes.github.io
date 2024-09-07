---
layout: distill
title: ParaView Installation
description: Installation of ParaView v5.13.0 on Ubuntu 24.04 LTS and Windows 11.
tags: Install
categories: ParaView
giscus_comments: false
date: 2024-08-18
featured: true

bibliography: 2024-08-18-ParaView-install.bib

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
  - name: ParaView on Win 11
  - name: ParaView on Ubuntu
  - subsections:
      - name: App Center
      - name: Binaries
---

## Introduction

In this post, I will go through the installation process of ParaView-5.13.0 on Windows 11 and Ubuntu 24.04 LTS.

ParaView is a wonderful open-source tool for data post-processing. Despite being an open-source project, it is a true competitor to other proprietary data visualization tools. It offers a user-friendly GUI and well-written documentation. It can be used effortlessly for everyday data post-processing, but you can go further and automate your post-processing workflow using the Python shell, which is also included in the ParaView GUI. Additionally, you can even run this tool in parallel on an HPC cluster.

---

## ParaView on Win 11

I would not recommend installing ParaView via WSL. The easiest way to get ParaView working on Windows 11 is to download the zip file of binaries fow Windows from [paraview.org/download](https://www.paraview.org/download/). You will have two options for downloading. For example, in the case of version 5.13.0, you will find the following zipped binaries:

- ParaView-5.13.0-Windows-Python3.10-msvc2017-AMD64.zip,
- ParaView-5.13.0-MPI-Windows-Python3.10-msvc2017-AMD64.zip.

The MPI version is intended for running ParaView in parallel. Initially, you will be completely fine with the version without MPI <d-cite key="ParaView_MPI"></d-cite>.

Place the zip file in a location with a short file path and unpack it. However, you may still encounter the error "Path too long."

{% details Path too long error %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-18-ParaView-Install/PathTooLong.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

In that case, rename the destination folder where the files will be extracted from the default zip file name to something shorter, such as "ParaView".

{% details Extract destination %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-18-ParaView-Install/ExtractDestination.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

After you successfully extract the zip file, navigate to the "bin" folder inside the unzipped directory and run "paraview.exe" as an administrator. If the blue "Windows protected your PC" window pops up, click on "More info" and then on "Run anyway".

{% details Did Windows protected your PC? %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/2024-08-18-ParaView-Install/WinProtected_1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/2024-08-18-ParaView-Install/WinProtected_2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

{% enddetails %}

You should now be able to run ParaView.

{% details ParaView on Win %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-18-ParaView-Install/InstalledParaView.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
{% enddetails %}

## ParaView Install on Ubuntu

### App Center

Probably the most easier way how to install ParaView on Ubuntu would be to install it from Ubuntu App Center. Unfortunatelly there are some drawbacks on this approach. There are is not available the newest version of ParaView and you cannot choose whether MPI will be enabled or not, or any other further options as enabling CUDA and so on.

Regarding the ParaView version, the current release is v5.13.0 and in App Center you will find only 5.11.2 release. The same situation is when you will install paraview via apt.

```bash
sudo apt install paraview
```

Newer version can be installed from Flathub.

{% details App Center and Flathub %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/2024-08-18-ParaView-Install/ParaView_App_Center.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/2024-08-18-ParaView-Install/ParaView_Flathub.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

{% enddetails %}

I probably wouldn't recommend this option, as it is not even an official way to get ParaView. These packages are probably not even directly maintained by Kitware, which isn't necessarily a bad thing, but if you encounter any problems with the installation and need to ask for help on the ParaView discourse, you will likely be directed to download ParaView from their website or GitHub (or GitLab) anyway, which is understandable.

### Binaries

You can download a compressed archive of the binaries for Linux from [paraview.org/download](https://www.paraview.org/download/). Ideally, you should unzip the .tar.gz file, navigate to the bin folder, and execute the paraview executable file.

{% details GUI ParaView Run %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-18-ParaView-Install/GUI_Run_ParaView.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

{% enddetails %}

If you attempted to run it via the GUI by double-clicking on the "paraview" file (or right-clicking and selecting "Run"), and nothing happened, try running it via the terminal. While this may not resolve the issue, it will show you an error message.

Simply navigate in therminal to that directory where is "paraview" executable and run it.

```bash
./paraview
```

{% details Running ParaView via terminal %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-18-ParaView-Install/RunningParaviewViaTerminal.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

{% enddetails %}

On Ubuntu 24.04 LTS I have received this error:

> qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in " " even though it was found.
> This application failed to start because no Qt platform plugin could be initialized.
> Reinstalling the application may fix this problem.
> \
> \
> Available platform plugins are: xcb.
> \
> \
> error: exception occured: Subprocess aborted
> {: .block-danger }

If we search in the ParaView Discourse FAQ, we find a solution to this error, which involves installing the xcb packages <d-cite key="ParaView_xcb_packages"></d-cite>.

```bash
sudo apt install libxcb-xinerama0 libxcb-xinput0
```

This solved the mentioned error, and it was possible to successfully run ParaView v5.13.0.

{% details ParaView from binaries on Ubuntu %}

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2024-08-18-ParaView-Install/RunningParaViewBinaries.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

{% enddetails %}
