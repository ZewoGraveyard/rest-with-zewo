# Introducing Zewo

Zewo is a project originally created by Paulo Faria, a developer based in
Curitiba, Brazil. Like Swift, Zewo is an open source project hosted in
GitHub. Today, the project is maintained by many other developers. It is a very
active project.

Zewo is not a framework, but a set of self-contained modules you can use
separately or together to create rich server-side software easily. This modular
architecture let you add to your project solely components you need, instead of
loading an entire set of libraries.

The modular design have a lot of benefits. You can integrate your code easily
with other frameworks or libraries and still benefit of the real power of Zewo:
coroutines. Zewo is built on coroutines in order to achieve concurrent
code. Coroutines is a principle coined by Melvin Conway back in 1958. It is a
way to accomplish multi-tasking without being preemptive. It means that a
routine is capable to stop its execution at certain points, and resuming later
at the point it was stopped.

Coroutine is a very important concept in Zewo and it is important to understand
its consequences in order to fully take advantage of it. A coroutine is also
known as green threads. But, unlike a common thread, a coroutine is not
parallel. It means that a coroutine executes along with other coroutines
concurrently, but not in parallel. One coroutine is executed at a time, which
mean that you will never need to worry about race conditions, locks and dead
locks.

What Zewo accomplishes is a concurrent execution of your code, not a parallel
execution. It is a quite different concept. To understand this concept, let’s
take a look on modern operating systems and how they perform on different
hardware architectures. First, let’s consider a unix operating system running on
a single processor machine. Unix is known to be a multi-task, multi-user
operating system.

On a single processor machine, the unix kernel works concurrently in order to
make it possible to run several processes. In fact, the kernel stipulates an
arbitrary amount of time each process will gain to execute themselves. Once this
time is expired, the process is suspended and other process is given the
opportunity to run and so forth. This way makes it possible to give the
impression that all things are running at the same time, since context switching
is really fast on modern hardware.

So, concurrency is a way to multi-task. Each task runs on the processor and than
is suspended, passing the processing to another task. The unix kernel is then
responsible to maintain each process state in order to resume it
later. Processes cannot make any assumption when they will be suspended since
this is something that is the operating system kernel responsibility.

But, what if we add another processor on a system like this, making it a
two-processor machine? So, the unix kernel can execute processes in parallel,
one on each processor. So, processes will effectively execute two at a time, not
one at a time like in a single processor machine.

Coming back to coroutines, you can understand it as a context switch that will
happen on a certain point of your code, which will let another piece of code to
execute in order to accomplish something. But one piece of code is executed at a
time. Unlike threads, your code chooses when to stop and give the opportunity to
another piece of code to execute. You can do it with threads, off course, but
usually you don’t mind about it and make your code as much parallel as possible
in order to minimize synchronizations and locks, which is a pain in parallel
code.

In short: concurrent is when you *take care* of a lot of things at once, and
parallel is when you *do* a lot of things at once. Zewo team preferred to use
coroutines because its several benefits:

- It runs on user space. So, you don't need to rely on system calls in order to
  achieve concurrency, which is far more efficient in terms of performance.

- You can design your code to suspend in points where you determine. So, your
  code is suspended deterministically instead of being suspended arbitrarily.

- You don't need to worry about dead locks, race conditions and critical
  sections. Everything runs on the same thread, so it is easier to design your
  code.

Well, its enough for now. Let's start working.

## Setting things up

Let's setup our development environment. You will need the following software:

- GIT, for source control;

- Swift compiler and command line tools.

### Installing for macOS

If you use a macOS, swift compiler and command line tools are bundled with
Xcode. However, it is a good idea start with `swiftenv`, a very simple command
line tool that helps you maintain several version of swift installed on your
machine.

In order to install _swiftenv_, you can use _homebrew_ package manager as follows:

`brew install kylef/formulae/swiftenv`

### Installing for Linux

_swiftenv_ is a set of shell scripts. Therefore, installing on linux is pretty
straightforward. It is a manual process, but simple enough to accomplish in a
few minutes.

First, you need to download the set of shell scrits. You do it by using _git_:

`git clone https://github.com/kylef/swiftenv.git ~/.swiftenv`

_swiftenv_ shell scripts need to be installed as instructed. They need the
_.swiftenv_ directory to be created and be located on your home folder.

Once you have installed it, it is time to configure. All you need to do is to
add a few lines to your .profile or .bash_profile. You will need to check which
startup file your shell loads at startup in order to set your environment. Some
linux distros have different ways to accomplish it. So, stick with your distro's
documentation in order to do it.

Well, that said, here is what you need to do in your _.profile_ or
`.bash_profile`. This example is assuming you have .bash_profile.

```bash
echo 'export SWIFTENV_ROOT="$HOME/.swiftenv"' >> ~/.bash_profile
echo 'export PATH="$SWIFTENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(swiftenv init -)"' >> ~/.bash_profile
```

That's it. Reload your .bash_profile and be happy.

### Installing swift with swiftenv

All you need to do is to execute the following command line. As of its writting,
the current version of swift is 3.0.2.

`swiftenv install 3.0.2`

After installing, check if it is working:

`swift --version`

You should see something like this (this is an output from a macOS system):

`Apple Swift version 3.0.2 (swiftlang-800.0.63 clang-800.0.42.1)
Target: x86_64-apple-macosx10.9`

So far, so good. 

## Our first Zewo program

Zewo is designed to be distributed using swift package manager. So, lets startup
creating a sample program in order to have a simple startup.

First, we need to create a new software package using swift packager. In order
to do so, open a terminal and create a directory. Assuming that you have _bash_
as your shell, it may look like this:

```bash
$ mkdir ZewoSample
$ cd ZewoSample
$ swift package init --type executable
```

The command `swift package init --type executable` will create a skelleton for
an application. It creates a standard directory structure to hold both your code
and your automated tests. Also, it creates a file called `Package.swift` which
contains information about your application. Let's take a look at it.

```swift
import PackageDescription

let package = Package(
    name: "ZewoSample"
)
```

This configuration file is no different from any other swift source code. It
creates a package, which is an object that describes your software. Up to this,
you said nothing about Zewo. You just said to swift packager that you have a
nice software called `ZewoSample`, nothing else.

Now it is time to tell swift packager about Zewo. After editing your
_Package.swift_ file may look like this:

```swift
import PackageDescription

let package = Package(
    name: "ZewoSample",
    dependencies: [
        .Package(url: "https://github.com/Zewo/HTTPServer.git", majorVersion: 0, minor: 14),
    ]
)
```

So, get back to the command line and instruct swift packager to download all of
its dependencies:

`swift package fetch`

Time to get a cup of coffee.


