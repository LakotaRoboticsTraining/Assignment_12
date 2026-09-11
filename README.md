# Lesson 12: Intro to WPILib and the Robot Project

Goal: Recognize the pieces of an FRC Java project and how the robot program starts and runs.

Time: About 40–50 minutes (plus opening the project with a mentor)

You will learn:

- What WPILib is
- How robot Main differs from training Main
- TimedRobot and the robot life-cycle methods (robotInit, teleopPeriodic, …)
- Where to look in the team project (frc.robot)
- Simulation vs a real roboRIO (high level)
Before this lesson: Lessons 1–11 (especially classes, inheritance, packages, methods).

### Why this matters

Everything you practiced — main, classes, methods, if, loops, packages — is still here. WPILib adds robot-specific types and a loop that runs many times per second while the match is on.

### What is WPILib?

WPILib is the official FRC software library: motors, joysticks, commands, timers, SmartDashboard, and more.

You install WPILib VS Code (VS Code + Java + FRC extensions + tools). Mentors will help with that once.

### How the program starts

Training programs looked like:

```java
public static void main(String[] args) {
    // your code
}
```



In a WPILib project, Main still has main, but it starts the robot framework:

```java
public static void main(String... args) {
    RobotBase.startRobot(Robot::new);
}
```



You almost never put match logic in Main. Logic lives in Robot and in subsystems/commands.

```java
Read that as: “Build a Robot object and let WPILib run it.” (Robot::new is a way to say “use the Robot constructor” — you do not need the :: syntax yourself yet.)
```

### Robot extends TimedRobot

```java
public class Robot extends TimedRobot {
    @Override
    public void robotInit() { ... }
    @Override
    public void teleopPeriodic() { ... }
}
```



This is inheritance + override (Lessons 9–10). WPILib calls these methods at the right time.

while (true) for the match loop.

On this team’s project, robotPeriodic() runs CommandScheduler.getInstance().run(); — that is what makes commands execute. You will use that in Lesson 13.

### Tour the team project

Have a mentor open 2026RobotProject. Find:

You are reading, not rewriting the whole robot today.

### Simulation vs real robot

● Simulation (desktop): practice logic without a roboRIO

● Deploy: send code to the robot computer (roboRIO) on the robot

Mentors will show deploy/driver station when you are on the bot.

### Printing on a robot

```java
System.out.println still works (Driver Station console / rioLog). Later you will also use dashboard widgets. Same idea as Lesson 1: print to see what the code is doing.
```

### Common first-day confusion

1. Looking for a big while loop in main — the loop is inside WPILib (periodic)

2. Editing Main for robot behavior — edit Robot, subsystems, or commands instead

3. Mixing teleop and auton code in one pile — use the matching *Init / *Periodic (or commands)

4. Changing constants in three places that prefer constants classes

## Try it yourself

Open a WPILib project with your mentor. Written answers are enough unless told otherwise.

### Challenge 1 â€” Main in WPILib

In your own words: what does `Main.main` do in a WPILib project vs these training assignments?

### Challenge 2 â€” Robot lifecycle methods

Open `Robot.java`. List three `@Override` methods you see and when each runs.

### Challenge 3 â€” Find examples

Find one subsystem class and one command class. Write the package of each.

### Challenge 4 â€” Optional (with mentor)

Run simulation, add one `System.out.println` in `robotInit`, and find that line in the console.

### Check your understanding

1. What library provides TimedRobot?

2. Who calls teleopPeriodic() — you, or WPILib?

3. Where should most robot behavior live: Main or subsystems/commands?

4. What does robotInit vs teleopPeriodic mean?

Answers

1. WPILib.

2. WPILib (the framework), many times per second during teleop.

3. Subsystems and commands (and sometimes Robot setup).

4. robotInit = once at startup; teleopPeriodic = repeatedly while drivers have control.

### Looking ahead

In Lesson 13, you will connect subsystems (hardware) and commands (actions) and sketch your first robot behavior the way this team’s code is structured.

Lesson complete. When you can find Main, Robot, a subsystem, and a command in the project, you are ready for Lesson 13.
