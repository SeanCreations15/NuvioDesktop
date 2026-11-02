# Linux controls rendering evidence

Synthetic 1280×720/24 fps colour-pattern clip, shown in a 5760×3094 Xwayland
player window. No private media, stream URLs or account data are included.

Both cases used GDK_SCALE=2 and mpv x11/GLX. A temporary harness kept controls
visible using a user stylesheet and kept overlay composition active, without
changing control geometry. The screenshots compare the same artificial scaling
condition. This is not a representation of the tester's normal app UI scale.

Before: native bridge from Dev 1a600da8. After: focused logical-resolution
controls candidate rebased on the same Dev commit. Each was embedded into an
isolated 0.1.33-alpha AppImage shell with separate empty configuration; this is
not a full packaged 0.1.34-alpha app test. Native libraries were rebuilt with
C++17/O2 against the same installed GTK/WebKit/mpv libraries.

The timing files contain 30-frame batch averages from temporary diagnostic
instrumentation. They are short samples, not a controlled cross-platform
benchmark. The artificial scale-2 workload was visibly much larger than the
user's normal UI, and other desktop applications were running.

Original snapshot: 5760×3094. Candidate snapshot: 2880×1546, displayed at the
same viewport size. The odd final row is stretched with the rest of the bitmap.
The candidate trades HiDPI controls sharpness for less snapshot/upload work;
video resolution is unchanged.

Both cases opened and displayed synthetic video and controls. At least one
baseline shutdown and an earlier candidate shutdown emitted a native Mesa
SIGSEGV marker; its cause has not been established. The final candidate run
reported no fault marker. No full crash dump is included here.

The interactive half-resolution prototype was separately tested in normal
playback/screen sharing and improved responsiveness, with clicks confirmed
aligned. The extracted automatic-scaling candidate still needs broader input,
GTK scale 1, mixed-monitor, resize/fullscreen and lifecycle testing.
