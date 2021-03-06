Known Issues
============

This document lists known commonly occurring issues and possible solutions.

.. _known-issue-window-tray-hidden:

On Windows, tray icon is hidden/repositioned after restart
----------------------------------------------------------

With current official builds of CopyQ, the tray icon position and hide/show
status are not restored after the application is restarted or after logging in.

**Workaround** is to use CopyQ binaries build with older Qt framework version (Qt
5.9); these are provided in latest comments in the issue link below.

.. seealso::

    `Issue #1258 <https://github.com/hluk/CopyQ/issues/1258>`__

.. _known-issue-macos-paste-after-install:

On macOS, CopyQ won't paste after installation/update
-----------------------------------------------------

CopyQ is not signed app, you need to grant Accessibility again when it's
installed or updated.

**To fix this**, try following steps:

1. Go to System Preferences -> Security & Privacy -> Privacy -> Accessibility
   (or just search for "Allow apps to use Accessibility").
2. Click the unlock button.
3. Select CopyQ from the list and remove it (with the "-" button).

.. seealso::

    - `Issue #1030 <https://github.com/hluk/CopyQ/issues/1030>`__
    - `Issue #1245 <https://github.com/hluk/CopyQ/issues/1245>`__

.. _known-issue-wayland:

On Linux, global shortcuts and pasting doesn't work
---------------------------------------------------

This can be caused by running Wayland instead of the old X11.

Wayland doesn't support:

- global shortcuts
- clipboard access from window that is not active
- mouse selection copy/pasting
- pasting from CopyQ (i.e. passing shortcuts to application)

**Workaround** for most problems is to set ``QT_QPA_PLATFORM`` environment variable
and use Xwayland (e.g. ``xorg-x11-server-Xwayland`` Fedora package).

E.g. launch CopyQ with::

    env QT_QPA_PLATFORM=xcb copyq

If CopyQ autostarts, you can change ``Exec=...`` line in
``~/.config/autostart/copyq.desktop``::

    Exec=env QT_QPA_PLATFORM=xcb copyq

.. note::

    Mouse selection will still work only if the source application itself
    supports it.

.. seealso::

    `Issue #27 <https://github.com/hluk/CopyQ/issues/27>`__
