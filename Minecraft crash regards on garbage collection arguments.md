 I just wanted to enhance the performance and experience of my minecraft client, so I... have played with JVM arguments and stuff. I could not run the game since it was crashing before showing me the menu screen.

# Environment

* modpack: ATM9, version 0.2.51
* forge version: 47.2.21
* Installed through Curseforge
* I let the curseforge's settings related to java as default, the only thing I have changed is keybinding to sprint and crouch.
* Used custom java location, openjdk17 and GraalVM for jdk17.
* RAM size is a maximum of 64Gb, so I allocated 32G as the maximum memory that Minecraft can use.

# Procedure

I tried variations with JDK and flags to run the Minecraft client.

## G1GC

## Skipping java runtime version check

* Set the java executable to javaw.exe of openjdk17, and check the skip java runtime version check
* Tried with the G1GC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G   
\-XX:+UseG1GC   
\-XX:MaxGCPauseMillis=37   
\-XX:+PerfDisableSharedMem   
\-XX:G1HeapRegionSize=16M   
\-XX:G1NewSizePercent=23   
\-XX:G1ReservePercent=20   
\-XX:SurvivorRatio=32   
\-XX:G1MixedGCCountTarget=3   
\-XX:G1HeapWastePercent=20   
\-XX:InitiatingHeapOccupancyPercent=10   
\-XX:G1RSetUpdatingPauseTimePercent=0   
\-XX:MaxTenuringThreshold=1   
\-XX:G1SATBBufferEnqueueingThresholdPercent=30   
\-XX:G1ConcMarkStepDurationMillis=5.0   
\-XX:G1ConcRSHotCardLimit=16   
\-XX:G1ConcRefinementServiceIntervalMillis=150   
\-XX:GCTimeRatio=99

## Result

* The game crashed instantly and showed me this error pop-up.

Error: Could not create the Java Virtual Machine.  
Error: A fatal exception has occurred. Program will exit.

## Not skipping java runtime version check

* Set the java executable to javaw.exe of openjdk17, and I **did not** check the skip java runtime version check
* Tried with the G1GC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G   
\-XX:+UseG1GC   
\-XX:MaxGCPauseMillis=37   
\-XX:+PerfDisableSharedMem   
\-XX:G1HeapRegionSize=16M   
\-XX:G1NewSizePercent=23   
\-XX:G1ReservePercent=20   
\-XX:SurvivorRatio=32   
\-XX:G1MixedGCCountTarget=3   
\-XX:G1HeapWastePercent=20   
\-XX:InitiatingHeapOccupancyPercent=10   
\-XX:G1RSetUpdatingPauseTimePercent=0   
\-XX:MaxTenuringThreshold=1   
\-XX:G1SATBBufferEnqueueingThresholdPercent=30   
\-XX:G1ConcMarkStepDurationMillis=5.0   
\-XX:G1ConcRSHotCardLimit=16   
\-XX:G1ConcRefinementServiceIntervalMillis=150   
\-XX:GCTimeRatio=99

## Result

* The game crashed instantly and showed me this error pop-up.

Error: Could not create the Java Virtual Machine.  
Error: A fatal exception has occurred. Program will exit.

## G1GC (with GraalVM)

## Skipping java runtime version check

* Set the java executable to javaw.exe of GraalVM 17 Enterprise edition, and I check the skip java runtime version check
* Tried with the G1GC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G  
\-XX:+UnlockExperimentalVMOptions   
\-XX:+UnlockDiagnosticVMOptions   
\-XX:+AlwaysActAsServerClassMachine   
\-XX:+AlwaysPreTouch   
\-XX:+DisableExplicitGC   
\-XX:+UseNUMA   
\-XX:AllocatePrefetchStyle=3   
\-XX:NmethodSweepActivity=1   
\-XX:ReservedCodeCacheSize=400M   
\-XX:NonNMethodCodeHeapSize=12M   
\-XX:ProfiledCodeHeapSize=194M   
\-XX:NonProfiledCodeHeapSize=194M   
\-XX:-DontCompileHugeMethods   
\-XX:+PerfDisableSharedMem   
\-XX:+UseFastUnorderedTimeStamps   
\-XX:+UseCriticalJavaThreadPriority   
\-XX:+EagerJVMCI   
\-Dgraal.TuneInlinerExploration=1   
\-Dgraal.CompilerConfiguration=enterprise

## Result

* The client has started,but when the game was almost loaded, it crashed and showed me this message.

The game crashed whilst rendering overlay  
Error: java.lang.RuntimeException: null

* crash report: [Pastebin](https://pastebin.com/TLqG9csv)

## Not skipping java runtime version check

* Set the java executable to javaw.exe of GraalVM 17 Enterprise edition, and I *did not* check the skip java runtime version check
* Tried with the G1GC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G  
\-XX:+UnlockExperimentalVMOptions   
\-XX:+UnlockDiagnosticVMOptions   
\-XX:+AlwaysActAsServerClassMachine   
\-XX:+AlwaysPreTouch   
\-XX:+DisableExplicitGC   
\-XX:+UseNUMA   
\-XX:AllocatePrefetchStyle=3   
\-XX:NmethodSweepActivity=1   
\-XX:ReservedCodeCacheSize=400M   
\-XX:NonNMethodCodeHeapSize=12M   
\-XX:ProfiledCodeHeapSize=194M   
\-XX:NonProfiledCodeHeapSize=194M   
\-XX:-DontCompileHugeMethods   
\-XX:+PerfDisableSharedMem   
\-XX:+UseFastUnorderedTimeStamps   
\-XX:+UseCriticalJavaThreadPriority   
\-XX:+EagerJVMCI   
\-Dgraal.TuneInlinerExploration=1   
\-Dgraal.CompilerConfiguration=enterprise

## Result

* The client has started,but when the game was almost loaded, it crashed and showed me this message.

The game crashed whilst rendering overlay  
Error: java.lang.RuntimeException: null

* crash report: [Pastebin](https://pastebin.com/KdhC1Lzp)

## ZGC

## Skipping java runtime version check

* Set the java executable to javaw.exe of openjdk17, and check the skip java runtime version check
* Tried with the ZGC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G  
\-XX:+UnlockExperimentalVMOptions   
\-XX:+UnlockDiagnosticVMOptions   
\-XX:+AlwaysActAsServerClassMachine   
\-XX:+AlwaysPreTouch   
\-XX:+DisableExplicitGC   
\-XX:+UseNUMA   
\-XX:NmethodSweepActivity=1   
\-XX:ReservedCodeCacheSize=400M   
\-XX:NonNMethodCodeHeapSize=12M   
\-XX:ProfiledCodeHeapSize=194M   
\-XX:NonProfiledCodeHeapSize=194M  
\-XX:-DontCompileHugeMethods   
\-XX:MaxNodeLimit=240000   
\-XX:NodeLimitFudgeFactor=8000   
\-XX:+UseVectorCmov   
\-XX:+PerfDisableSharedMem   
\-XX:+UseFastUnorderedTimeStamps   
\-XX:+UseCriticalJavaThreadPriority   
\-XX:ThreadPriorityPolicy=1   
\-XX:+UseZGC   
\-XX:AllocatePrefetchStyle=1   
\-XX:-ZProactive

## Result

* The client has started, but when the game was almost loaded, it crashed and showed me this message.

The game crashed whilst rendering overlay  
Error: java.lang.RuntimeException: null

* crash report: [Pastebin](https://pastebin.com/6Zn9wGQf)

## Not skipping java runtime version check

* Set the java executable to javaw.exe of openjdk17, and I *did not* check the skip java runtime version check
* Tried with the ZGC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G  
\-XX:+UnlockExperimentalVMOptions   
\-XX:+UnlockDiagnosticVMOptions   
\-XX:+AlwaysActAsServerClassMachine   
\-XX:+AlwaysPreTouch   
\-XX:+DisableExplicitGC   
\-XX:+UseNUMA   
\-XX:NmethodSweepActivity=1   
\-XX:ReservedCodeCacheSize=400M   
\-XX:NonNMethodCodeHeapSize=12M   
\-XX:ProfiledCodeHeapSize=194M   
\-XX:NonProfiledCodeHeapSize=194M  
\-XX:-DontCompileHugeMethods   
\-XX:MaxNodeLimit=240000   
\-XX:NodeLimitFudgeFactor=8000   
\-XX:+UseVectorCmov   
\-XX:+PerfDisableSharedMem   
\-XX:+UseFastUnorderedTimeStamps   
\-XX:+UseCriticalJavaThreadPriority   
\-XX:ThreadPriorityPolicy=1   
\-XX:+UseZGC   
\-XX:AllocatePrefetchStyle=1   
\-XX:-ZProactive

## Result

* The client has started, but when the game was almost loaded, it crashed and showed me this message.

The game crashed whilst rendering overlay  
Error: java.lang.RuntimeException: null

* crash report: [Pastebin](https://pastebin.com/wjujVmuX)

## Shenandoah GC

## Skipping java runtime version check

* Set the java executable to javaw.exe of openjdk17, and I check the skip java runtime version check
* Tried with the Shenandoah GC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G  
\-XX:+UseLargePages   
\-XX:LargePageSizeInBytes=2M   
\-XX:+UnlockExperimentalVMOptions   
\-XX:+UseShenandoahGC   
\-XX:ShenandoahGCMode=iu   
\-XX:+UseNUMA   
\-XX:+AlwaysPreTouch   
\-XX:-UseBiasedLocking   
\-XX:+DisableExplicitGC

## Result

* The game crashed instantly and showed me this error pop-up.

Error: Could not create the Java Virtual Machine.  
Error: A fatal exception has occurred. Program will exit.

## Not skipping java version check

* Set the java executable to javaw.exe of openjdk17, and I check the skip java runtime version check
* Tried with the Shenandoah GC flag below in the launcher's settings

\-Xms30G  
\-Xmx32G  
\-XX:+UseLargePages   
\-XX:LargePageSizeInBytes=2M   
\-XX:+UnlockExperimentalVMOptions   
\-XX:+UseShenandoahGC   
\-XX:ShenandoahGCMode=iu   
\-XX:+UseNUMA   
\-XX:+AlwaysPreTouch   
\-XX:-UseBiasedLocking   
\-XX:+DisableExplicitGC

## Result

* The game crashed instantly and showed me this error pop-up.

Error: Could not create the Java Virtual Machine.  
Error: A fatal exception has occurred. Program will exit.

## Default settings

## Procedure

* I set every setting to default
* Restarted the machine, and let Curseforge deal with everything.

## Result

* The client has started, but when the game was almost loaded, it crashed and showed me this message.

The game crashed whilst rendering overlay  
Error: java.lang.RuntimeException: null

* crash report: [Pastebin](https://pastebin.com/RKtdTGCu)

Whoa, it's **A LOT**. But I wanted to deliver every single detail so that somebody please be able to find the solution.

# In short

* I tried G1GC, G1GC with GraalVM, ZGC, and Shenandoah GC to run minecraft
* None of them worked and now I cannot even play with default settings
* I tried G1GC, G1GC with GraalVM, ZGC, and Shenandoah GC to run Minecraft, but everything had failed.  What could be the best solution to play it again apart from re-installing?  I want to enhance the performance.