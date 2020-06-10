AudioServer
===================

AudioServer is the primary process that hosts several audio related services. It runs as a daemon throughout the lifetime of the device. Below is the high level architecture of android audio server.

.. uml:: high_level_block_diagram.puml

This process is launched at startup by the Android init system. Init script can be found under `audioserver.rc <https://android.googlesource.com/platform/frameworks/av/+/master/media/audioserver/audioserver.rc>`_. 

.. code-block:: Bash
    :linenos:
    :emphasize-lines: 3-8

    service audioserver /system/bin/audioserver
        class core
        user audioserver
        # media gid needed for /dev/fm (radio) and for /data/misc/media (tee)
        group audio camera drmrpc inet media mediadrm net_bt net_bt_admin net_bw_acct wakelock
        capabilities BLOCK_SUSPEND
        ioprio rt 4
        writepid /dev/cpuset/foreground/tasks /dev/stune/foreground/tasks
        onrestart restart vendor.audio-hal-2-0
        onrestart restart vendor.audio-hal-4-0-msd
        # Keep the original service name for backward compatibility when upgrading
        # O-MR1 devices with framework-only.
        onrestart restart audio-hal-2-0

The audioserver process is started with user ``audioserver``. It belongs to several groups listed in line number 5. Line number 7 sets the io priority of the audioserver process. Init process sets the priority class to ``Realtime`` and sets the priorty to 4. Line number 8 is for adding the audioserver process to cgroup cpuset foreground.

