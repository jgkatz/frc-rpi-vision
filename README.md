# frc-rpi-vision
Raspberry Pi Vision Experiments for FRC

# Steps to get to this point

Based on https://wpilib.screenstepslive.com/s/currentCS/m/vision/l/687863-off-board-vision-processing-in-java

If you have the Raspberry Pi connected to the web you can perform these steps
on the box itself.

1. Set up a new folder for development. In that folder, clone this project:

```
git clone https://github.com/jgkatz/frc-rpi-vision.git
```

I originally set up the project by pulling in the vision sample code from FRC
at https://github.com/wpilibsuite/VisionBuildSamples.git, then configured
build.gradle for arm-raspbian and main.java for a usb camera.

2. For some reason the example build.gradle does not include the dependencies
necessary for running the vision pipeline. In build.grade, change

```
dependencies {
  compile ntcoreDep()
  compile cscoreDep()
  compile 'org.opencv:opencv-java:3.1.0'
}
```

to

```
dependencies {
  compile ntcoreDep()
  compile cscoreDep()
  compile 'org.opencv:opencv-java:3.1.0'
  // This next line adds the latest wpilib artifact
  compile 'edu.wpi.first.wpilibj:athena:+'
}
```

3. Add the pipeline code to the project

```
cd Java/src/main
mkdir gripvision
```

Copy the generated pipeline code into the folder. There's an existing one
there already.

4. If you're not running on the robot network you might want to comment out
the code that connects to the NetworkTable server in main.java

```
    // Connect NetworkTables, and get access to the publishing table
    // NetworkTable.setClientMode();
    // // Set your team number here
    // NetworkTable.setTeam(9999);

    // NetworkTable.initialize();

```

5. After that should be possible to build and run:

```
./gradlew build
cd output
sh runCameraVision
```
