## Notes
- The .bashrc will ONLY run what is in it if you start a container with a bash shell.

## Errors and solutions

### Error: MESA-LOADER
<pre>
libGL error: MESA-LOADER: failed to retrieve device information
libGL error: Version 4 or later of flush extension not found
libGL error: failed to load driver: i915
libGL error: failed to open drm device: No such file or directory
libGL error: failed to load driver: i965
</pre>

Solution: Add following when running a container.
<pre>
--device=/dev/dri:/dev/dri
</pre>

### Error: dbus issues
Solution: add following to Dockerfle
<pre>
RUN apt-get install dbus dbus-x11
# adding the export to .bashrc fixes a bug
# -> https://bugs.launchpad.net/ubuntu/+source/at-spi2-core/+bug/1193236
# -> https://unix.stackexchange.com/questions/230238/starting-x-applications-from-the-terminal-and-the-warnings-that-follow
RUN echo 'export NO_AT_BRIDGE=1' >> /home/user/.bashrc
</pre>


