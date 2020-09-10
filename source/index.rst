Android Audio Documentation!
============================

Introduction
------------

Welcome to Android audio documentation site. This site was created to provide design and implementation details of Android Audio stack.

From an Android application developers perspective, Android Audio API's are very well documented. Android platform implementor would be interested in understanding the various modules within the Android stack involved in audio handling.Android audio stack is really complex involving many different libraries. Android documentation of audio available at `source.android.com <https://source.android.com/devices/audio>`_  is a good starting point. But it lacks a lot of details. 

This page attempts to demystify the inner workings of Android audio stack and tries to document various components and interfaces. Speficially, we look at following components of the android audio stack:

*  Android Audioserver.
*  Android Audioflinger.
*  Android Audio policy manager.
*  AAudio client and service.
*  Sound Trigger Client and HAL.
*  Audio HAL.

It also attempts to help a detailed guide on developing a custom audio HAL.

.. toctree::
   :maxdepth: 1
   :caption: Table of Contents:

   audioserver/audioserver
   audioflinger/audioflinger
   effects/android_effects
   aaudio/aaudio

Android Audio stack
-------------------
Android audio stack is built on top on Linux ALSA(Advanced Linux Sound Arhitecture) infrastructure. The ALSA driver lives within the Linux kernel space. Android Audio HAL is a userspace process. It's the lower most component within usersapce. It uses library called `tinyalsa <https://android.googlesource.com/platform/external/tinyalsa/+/master/>`_ to access the ALSA driver in kernel. Android audio server includes AAudioService, AudioFlinger and AudioPolicyManager.  AAudioService and AudioFlinger binder based interfaces with Audio HAL to read and write audio streams. Android provides two libraries AAudioClient and libaudioclient to access AAudioService and AudioFlinger. Finally, for Java applications interact with audio services through a JNI interface.

Below is a diagram depicts the android audio stack:

.. uml:: android_audio_stack.puml

Indices and tables
==================

* :ref:`genindex`
* :ref:`search`
