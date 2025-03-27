# Retirement notice

I don't use this project anymore. Feel free to fork it.

# cs-dlp

This is a fork of [coursera-dl](https://github.com/coursera-dl/coursera-dl) that works with modern Python and modern coursera.org, with added features and patches.

<!-- [![Build Status](https://travis-ci.org/coursera-dl/coursera-dl.svg?branch=master)](https://travis-ci.org/coursera-dl/coursera-dl) -->
<!-- [![Build status](https://ci.appveyor.com/api/projects/status/3hru0ycv5fbny5k8/branch/master?svg=true)](https://ci.appveyor.com/project/balta2ar/coursera-dl/branch/master) -->
<!-- [![Coverage Status](https://coveralls.io/repos/coursera-dl/coursera-dl/badge.svg)](https://coveralls.io/r/coursera-dl/coursera-dl) -->
<!-- [![Latest version on PyPI](https://img.shields.io/pypi/v/coursera-dl.svg)](https://pypi.python.org/pypi/coursera-dl) -->
<!-- [![Code Climate](https://codeclimate.com/github/coursera-dl/coursera-dl/badges/gpa.svg)](https://codeclimate.com/github/coursera-dl/coursera-dl) -->

<!-- TOC -->

- [Coursera Downloader](#coursera-downloader)
- [Introduction](#introduction)
- [Features](#features)
- [Disclaimer](#disclaimer)
- [Installation instructions](#installation-instructions)
    - [Recommended installation method for all Operating Systems](#recommended-installation-method-for-all-operating-systems)
    - [Alternative ways of installing missing dependencies](#alternative-ways-of-installing-missing-dependencies)
        - [Alternative installation method for Unix systems](#alternative-installation-method-for-unix-systems)
        - [ArchLinux](#archlinux)
        - [Installing dependencies on your own](#installing-dependencies-on-your-own)
    - [Docker](#docker)
    - [Windows](#windows)
    - [Create an account with Coursera](#create-an-account-with-coursera)
- [Running the script](#running-the-script)
    - [Resuming downloads](#resuming-downloads)
- [Troubleshooting](#troubleshooting)
    - [China issues](#china-issues)
    - [Found 0 sections and 0 lectures on this page](#found-0-sections-and-0-lectures-on-this-page)
    - [Download timeouts](#download-timeouts)
    - [Windows: proxy support](#windows-proxy-support)
    - [Windows: Failed to create process](#windows-failed-to-create-process)
    - [SSLError: [Errno 1] _ssl.c:504: error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure](#sslerror-errno-1-_sslc504-error14094410ssl-routinesssl3_read_bytessslv3-alert-handshake-failure)
    - [Alternative CDN for `MathJax.js`](#alternative-cdn-for-mathjaxjs)
- [Reporting issues](#reporting-issues)
- [Filing an issue/Reporting a bug](#filing-an-issuereporting-a-bug)
- [Feedback](#feedback)
- [Contact](#contact)

<!-- /TOC -->

# Introduction

This script makes it easier to batch download lecture resources (e.g., videos, ppt,
etc) for [Coursera](coursera.org) classes.  Given one or more class names,
it obtains week and class names from the *lectures* page, and then downloads
the related materials into appropriately named files and directories.

This work was originally inspired in part by [youtube-dl][3] by which
I've downloaded many other good videos such as those from Khan Academy.


# Features

* Support for all kinds of courses (i.e., "Old Platform"/time-based as
    well as "New Platform"/on-demand courses).
* Intentionally detailed names, so that it will display and sort properly
    on most interfaces (e.g., VLC or MX Video on Android devices).
* Regex-based section (week) and lecture name filters to download only
    certain resources.
* File format extension filter to grab resource types you want.
* Default arguments loaded from `coursera-dl.conf` file.
* Core functionality tested on Linux, Mac and Windows.

# Disclaimer

`cs-dlp` is meant to be used only for your material that Coursera gives
you access to download.

We do not encourage any use that violates their [Terms Of Use](https://www.coursera.org/about/terms).
A relevant excerpt:

> "[...] Coursera grants you a personal, non-exclusive, non-transferable
> license to access and use the Sites. You may download material from the
> Sites only for your own personal, non-commercial use. You may not
> otherwise copy, reproduce, retransmit, distribute, publish, commercially
> exploit or otherwise transfer any material, nor may you modify or create
> derivatives works of the material."


# Installation instructions

`cs-dlp` requires Python 3 and a Coursera account enrolled in the class of interest.

**Note:** `cs-dlp` is not compatible with Python 2.

On any operating system, ensure that the Python executable location is added
to your `PATH` environment variable and, once you have the dependencies
installed (see next section), for a *basic* usage, you will need to invoke
the script from the main directory of the project and prepend it with the
word `python`.  You can also use more advanced features of the program by
looking at the "Running the script" section of this document.

*Note:* You must already have (manually) agreed to the Honor of Code of the
particular courses that you want to use with `cs-dlp`.

## Installing from source

From a command line (preferably, from a virtual environment), simply issue
the command:

    git clone https://github.com/raffaem/cs-dlp
    cd cs-dlp
    python -m pip install --user .

**Note 1:** We strongly recommend that you *don't* install the package
globally on your machine (i.e., with root/administrator privileges), as the
installed modules may conflict with other Python applications that you have
installed in your system. Prefer to use the option `--user` to `pip install`.

### ArchLinux

`cs-dlp` does not currently have an AUR package. Help welcome!

<!-- ## Docker -->

<!-- If you prefer you can run this software inside Docker: -->

<!-- ``` -->
<!-- docker run --rm -it -v \ -->
<!--     "$(pwd):/courses" \ -->
<!--     courseradl/courseradl -u <USER> -p <PASSWORD> -->
<!-- ``` -->

<!-- Or using netrc file: -->

<!-- ``` -->
<!-- docker run --rm -it \ -->
<!--     -v "$(pwd):/courses" -v "$HOME/.netrc:/netrc" \ -->
<!--     courseradl/courseradl -n /netrc -->
<!-- ``` -->

## Create an account with Coursera

If you don't already have one, create a [Coursera][1] account and enroll in
a class. See https://www.coursera.org/courses for the list of classes.

# Authenticating

To authenticate with Coursera, you need a CAUTH cookie.

There are currently two supported ways to do so: you can have `cs-dlp` get it automatically from your browser, or you can pass one manually.

1. Automatic way
    1. Open your favorite browser and login into Coursera
    2. Call `cs-dlp` with `--cauth-auto browser` option.
 
        Valid options for `browser` are:
    
        * `chrome` for Google Chrome
        * `chromium`
        * `opera`
        * `opera_gx`
        * `brave`
        * `edge`
        * `vivaldi`
        * `firefox`
        * `librewolf`
        * `safari`
2. Manual way

    Pass a CAUTH cookie to the `--cauth` option.
    

# Running the script

Refer to `cs-dlp --help` for a complete, up-to-date reference on the runtime options
supported by this utility.

Run the script to download the materials by providing your Coursera CAUTH cookie,
the class names, as well as any additional parameters:

```
cs-dlp --cauth-auto chrome modelthinking-004
```

Here are some examples of how to invoke `cs-dlp` from the command line:
```
    Multiple classes:            cs-dlp --cauth-auto chrome saas historyofrock1-001 algo-2012-002
    Filter by section name:      cs-dlp --cauth-auto chrome -sf "Chapter_Four" crypto-004
    Filter by lecture name:      cs-dlp --cauth-auto chrome -lf "3.1_" ml-2012-002
    Download only ppt files:     cs-dlp --cauth-auto chrome -f "ppt" qcomp-2012-001
    Get the preview classes:     cs-dlp --cauth-auto chrome -b ni-001
	Download videos at 720p:     cs-dlp --cauth-auto chrome --video-resolution 720p ni-001
    Specify download path:       cs-dlp --cauth-auto chrome --path=C:\Coursera\Classes\ comnetworks-002
    Display help:                cs-dlp --help

    Maintain a list of classes in a dir:
      Initialize:              mkdir -p CURRENT/{class1,class2,..classN}
      Update:                  cs-dlp -n --path CURRENT `\ls CURRENT`
```
**Note:** If your `ls` command is aliased to display a colorized output, you
may experience problems.  Be sure to escape the `ls` command (use `\ls`) to
assure that no special characters get sent to the script.

Note that we *do* support the New Platform ("on-demand") courses.

By default, videos are downloaded at 540p resolution. For on-demand courses, the
`--video-resolution` flag accepts 360p, 540p, and 720p values.

To download just the `.txt` and/or `.srt` subtitle files instead of the videos,
use `--ignore-formats mp4 --subtitle-language en` or whatever format the videos
are encoded in and desired languages for subtitles.

If you want to store your preferred parameters,
create a file named `coursera-dl.conf`
where the script is supposed to be executed, with the following format:
```
    --subtitle-language en,zh-CN|zh-TW
    --download-quizzes
    #--mathjax-cdn https://cdn.bootcss.com/mathjax/2.7.1/MathJax.js
    # more other parameters
```
Parameters which are specified in the file will be overriden if they are 
provided again on the commandline.

**Note:** In `coursera-dl.conf`, all the parameters should not be wrapped
with quotes.

## Resuming downloads

In default mode when you interrupt the download process by pressing
<kbd>CTRL</kbd>+<kbd>C</kbd>, partially downloaded files will be deleted from your disk and
you have to start the download process from the beginning. If your
download was interrupted by something other than KeyboardInterrupt
(<kbd>CTRL</kbd>+<kbd>C</kbd>) like sudden system crash, partially downloaded files will
remain on your disk and the next time you start the process again,
these files will be discarded from download list!, therefore it's your
job to delete them manually before next start. For this reason we
added an option called `--resume` which continues your downloads from
where they stopped:

	cs-dlp --cauth-auto chrome --resume sdn1-001

This option can also be used with external downloaders:

	cs-dlp --cauth-auto chrome --wget --resume sdn1-001

*Note 1*: Some external downloaders use their own built-in resume feature
which may not be compatible with others, so use them at your own risk.

*Note 2*: Remember that in resume mode, interrupted files **WON'T** be deleted from
your disk.

# Troubleshooting

If you have problems when downloading class materials, please try to see if
one of the following actions solve your problem:

* Make sure the class name you are using corresponds to the resource name
  used in the URL for that class:
    `https://www.coursera.org/learn/<CLASS_NAME>/home/welcome`

* Have you tried to clean the cached cookies/credentials with the
  `--clear-cache` option?

* Note that many courses (most, perhaps?) may remove the materials after a
  little while after the course is completed, while other courses may retain
  the materials up to a next session/offering of the same course (to avoid
  problems with academic dishonesty, apparently).
  <br><br>
  In short, it is not guaranteed that you will be able to download after the
  course is finished and this is, unfortunately, nothing that we can help
  you with.

* One can export a Netscape-style cookies file with a browser extension ([1][9], [2][10])
  and use it with the `-c` option. This comes in handy
  when the authentication via password is not working (the authentication
  process changes now and then).

<!-- * If results show 0 sections, you most likely have provided invalid -->
<!--   credentials (username and/or password in the command line or in your -->
<!--   `.netrc` file or in your `coursera-dl.conf` file). -->

* For courses that have not started yet, but have had a previous iteration
  sometimes a preview is available, containing all the classes from the last
  course. These files can be downloaded by passing the `--preview`
  parameter.

* If you get an error like `Could not find class: <CLASS_NAME>`, then:
    * Verify that the name of the course is correct. Current class
    names in coursera are composed by a short course name e.g. `class` and
    the current version of the course (a number). For example, for a
    class named `class`, you would have to use `class-001`, `class-002`
    etc.
    * Second, verify that you are enrolled in the course. You won't be
    able to access the course materials if you are not officially
    enrolled and agreed to the honor course *via the website*.

## China issues

If you are from China and you're having problems downloading videos,
adding "52.84.167.78 d3c33hcgiwev3.cloudfront.net" in the hosts file
(/etc/hosts) and freshing DNS with "ipconfig/flushdns" may work
(see https://github.com/googlehosts/hosts for more info).

## Found 0 sections and 0 lectures on this page

First of all, make sure you are enrolled to the course you want to download.

Many old courses have already closed enrollment so often it's not an
option. In this case, try downloading with `--preview` option. Some
courses allow to download lecture materials without enrolling, but
it's not common and is not guaranteed to work for every course.

Finally, you can download the videos if you have, at least, the index
file that lists all the course materials. Maybe your friend who is enrolled
could save that course page for you. In that case use the `--process_local_page`
option.

Alternatively you may want to try this various browser extensions designed for
this problem.

If none of the above works for you, there is nothing we can do.

## Download timeouts

cs-dlp supports external downloaders but note that they are only used to
download materials after the syllabus has been parsed, e.g. videos, PDFs, some
handouts and additional files (syllabus is always downloaded using the internal
downloader). If you experience problems with downloading such materials, you may
want to start using external downloader and configure its timeout values. For
example, you can use aria2c downloader by passing `--aria` option:

```
cs-dlp --cauth-auto chrome --path . --aria2  <course-name>
```

And put this into aria2c's configuration file `~/.aria2/aria2.conf` to reduce
timeouts:

```
connect-timeout=2
timeout=2
bt-stop-timeout=1
```

Timeout configuration for internal downloader is not supported.

## Windows: proxy support

If you're on Windows behind a proxy, set up the environment variables
before running the script as follows:

```
set HTTP_PROXY=http://host:port
set HTTPS_PROXY=http://host:port
```

Related discussion: [#205](https://github.com/coursera-dl/coursera-dl/issues/205)

<!-- ## SSLError: [Errno 1] _ssl.c:504: error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure -->

<!-- This is a known error, please do not report about this error message! The problem is in **YOUR** environment. To fix it, do the following: -->

<!-- ``` bash -->
<!-- sudo apt-get install build-essential python-dev libssl-dev libffi-dev -->
<!-- pip install --user urllib3 pyasn1 ndg-httpsclient pyOpenSSL -->
<!-- ``` -->
<!-- If the error remains, try installing coursera-dl from github following this instruction: -->
<!-- https://github.com/coursera-dl/coursera-dl#alternative-installation-method-for-unix-systems -->

<!-- If you still have the problem, please read the following issues for more ideas on how to fix it: -->
<!-- [#330](https://github.com/coursera-dl/coursera-dl/issues/330) -->
<!-- [#377](https://github.com/coursera-dl/coursera-dl/issues/377) -->
<!-- [#329](https://github.com/coursera-dl/coursera-dl/issues/329) -->

<!-- This is also worth reading: -->
<!-- https://urllib3.readthedocs.io/en/latest/security.html#insecureplatformwarning -->

## Alternative CDN for `MathJax.js`

When saving a course page, we enabled `MathJax` rendering for math equations, by
injecting `MathJax.js` in the header. The script is using a cdn service provided
by [mathjax.org](https://cdn.mathjax.org/mathjax/latest/MathJax.js). However, that
url is not accessible in some countries/regions, you can provide a
`--mathjax-cdn <MATHJAX_CDN>` parameter to specify the `MathJax.js` file that is
accessible in your region.

# Reporting issues

Before reporting any issue please follow the steps below:

1. Verify that you are running the latest version of the script

2. If the problem persists, feel free to [open an issue](https://github.com/raffaem/cs-dlp/issues) in our
bugtracker, please fill the issue template with *as much information as
possible*.

# Donations

You can support the project by sponsoring me:

<iframe src="https://github.com/sponsors/raffaem/button" title="Sponsor raffaem" height="32" width="114" style="border: 0; border-radius: 6px;"></iframe>
