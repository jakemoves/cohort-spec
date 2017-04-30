Cohort v3 Specification
=======================

Introduction
-----------------------
Cohort is a code framework that helps artists & activists do interesting things with groups of people. It allows creators to cue and play back synchronized or individually targeted audio, video, and augmented reality content on smartphones and tablets.

In the development of Cohort, the priority is to make it **useful** and **accessible**.

Useful means it should:

- do a few things, and not try to do 'all the things'
- integrate with existing tools (i.e. QLab, Isadora)
- be reliable enough for theatrical use
- be thoroughly tested on actual devices

Accessible means it should:

- be well-documented...
	* in the code, via comments
	* in technical documentation
	* via tutorials and guides
- prefer legibility over elegance in code style
- be quick to get started with
- be easy to work with
- have humans available for help and advice
- be taught via workshops
- include sample / demo projects
- be substantially open-source

While we don't have any ethical objection to generating revenue, it's not the main goal of this project. That said, we have identified a couple of components that could generate revenue to offset development and operational costs. It's important that these are 'convenience' components: using our mobile app instead of third-party software like QLab, or using our hosted server instead of self-hosting. 

User Stories
----------------------------------------------------
These reflect a range of potential uses for Cohort.

**Lianne** is an English indie choreographer with a freelance company. She’s working on an immersive theatre project set in a decommissioned coalmine and wants to embed earbuds in miners' helmets to play sound cues. She's worked with QLab before and she can do a little in Isadora. She's fundraising to buy a few iPod touches for users.

**Gerhardt** is a German theatre artist. He wants to do a roaming urban work with lots of audio and a little video, with no laptops involved. The audience will use their own devices and headphones.

**Janet** is a curator at a gallery. She wants to experiment with augmenting their current audio-tour system. Her idea is to use AR content to visually annotate featured works. The institution will supply a few devices to start, but eventually they would like to take advantage of guests' own devices.

**Kshama** is an activist who wants to experiment with “digital direct action” that uses AR in large-group settings. She wants to figure out a way to stage a 'statue-toppling', but with a 3D augmented-reality statue. It's important for her that participants can capture and share what they're seeing.

Each of these (imagined) users would use a different word to describe the people they're making things for: users, audience members, guests, patrons, participants, etc. For succinctness we will call the person making something with Cohort a 'user' and the person that they're making it for a 'guest'.

Non Goals
------------------------
We have had user interest in:

- cueing live audio

...but are not actively developing towards those features. Yet.

Components
------------------------
Cohort will require the following components to be developed in order to fulfill the user stories described above.

### Client
This is what runs on a guest's device and plays content. For cross-platform distribution and ease of use, we think it's best to build this as a Unity package, with a web-based fallback. It should have a very short 'time to first cue' — it should be quick for someone to try it out. In addition to cueing audio / video / AR, it needs to support:

- analytics
- in-app screenshot and video capture (so guests can share what they see on social media)

### Admin Client
This is how a user triggers cues and monitors guests' devices. We want to support:

- laptop-driven shows with QLab & Isadora interoperability
- fully mobile shows via a native app: either built with Unity (if we can leverage existing multiplayer functionality) or iOS native

The mobile version of this component could be revenue-generating without being prohibitive (i.e. $1-$5 on the App Store for the mobile app version).

### Cue Editor
This is how a user creates a cuelist for use with Cohort. We considered exporting from QLab, since many users know how to use it. But for first release it's probably best to make this web-based, exporting a JSON file.

### API / Protocol(s)
This defines how Cohort signals are transmitted over the network from a user to guests. It also defines the format of the cuelist or showbook.

- earlier versions used server-sent events
- probably time to move to sockets, so we can have a two-way connection with guest devices
- investigate mesh networking (so that a Cohort event is not dependent on external wifi or data)

### Server
This transmits Cohort signals from a user to guests.

- likely built with node.js
- can run on a laptop over WLAN 
- should include a simple GUI wrapper for friendly local use (maybe just a static webpage?)
- can run on a remote server over the internet
- we should host a server instance
- users can spin up their own server instances on their own hosting
- supports analytics

This component could be revenue-generating (i.e. a per-guest or per-event charge to use our hosted server).

### Documentation
This includes:

- technical / API documentation
- Cohort website
- tutorials and guides
- links to help with deploying to App Stores from Unity
- lessons learned: AR issues on Apple App Store
