# Preface

Writing about a technical subject is something that I have been dating for a
long time. Since the debut of my first book, which is an essay about my bad
experiences as a novice entrepreneur, I was looking forward to write some
technical material.

Since 2011 I’ve been involved with Apple, developing software for its iOS
platform. When swift was released, back in 2014, I got really interested in the
language due to its strong typing, easy namespace management and its nice
features, like optionals and optional chaining.

Last year Apple open sourced swift, letting it get into the main operating
system for servers: Linux. So, swift met Tux. And it gave to us, developers,
another powerful language to work with, a language powerful enough to be used
for server-side development.

Since its debut as an open source project, Swift language has becoming popular
in the back-end development scenario. Its modern characteristics, added to a
very simple and stable package manager for dependency management have made Swift
a natural choice for backend development.

Another important factor is the fact that a Swift backend software will execute
faster, with less footprint, since it is a real executable, not an interpreted
language. In addition, integrating a swift software with existing C and C++
libraries is simple and transparent, which gives to your backend software
excellent support to process scheduling, interprocess communication and a lot of
interesting operating system features.

But, starting writing software using swift from scratch will lead you to write a
lot of code. This is not because swift is a poor language, but because there are
few frameworks ready for portable code. Since Linux is the de facto standard for
server software nowadays, you will need to write a lot of basic code like HTTP
protocol implementation, socket management and so forth.

That’s where Zewo comes to place. It is not a framework, but a set of
self-contained modules that can be used to speed-up your development. Zewo
modules can be easily added to your project through Swift’s package
manager. Since it is open-sourced, you may want to read the code and understand
how its clockworks really work, which give to you more power to develop your
solutions.

Well, I wrote this little book as a contribution for the Zewo Project, a project
that I have embraced. I hope this material can lead you to start developing with
Zewo and help you write quality server-side code.

So, let’s begin!

Ronaldo

# How to read this book

This book was written as a tutorial, a step-by-step text which introduces
concepts as they are necessary. So, it was intended to be a book where you
should read from start to end. It is not a reference book, though. You should
have the patience to get into it as we travel through each concept and
functionality of Zewo amazing modules.

## Pre-requisites

This book starts from the premise that you know Apple's Swift language. If you
don't know swift, nor programming, it is a good idea to learn Swift language
first before going on.

To run the examples presented in this book you will need a linux or a macOS
box. Familiarity with command line is not required, but it is good to be
familiar with shell commands.





