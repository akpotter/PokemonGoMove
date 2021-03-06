# Pokemon GO GPS Emulator

This project uses Xcode Debug mode [Simulating a Location at Runtime](https://developer.apple.com/library/ios/recipes/xcode_help-debugger/articles/simulating_locations.html) to spoof GPS locations for non-jailbroken iOS devices. This allows players of Pokemon GO to send movement commands over a computer as opposed to doing the actual walking.

## Warning: Improper Use of this Tool Will Get You Banned!
As reported on [reddit](https://www.reddit.com/r/pokemongo/comments/4ry7my/psa_spoofing_gps_locations_will_get_you_banned/), spoofing your GPS coordinates in game could get you banned. Anecdotally, when you change your GPS coordinates drastically in a short period of time (say NYC to SF), you will be soft banned for anywhere between 10 mins to 3 hours. However, there have not been cases of permanent ban, so do this at your discretion. My guess is that the Niantic servers compute a delta distance over delta t and sets a threshold on the speed. Anything beyond the threshold will get your banned.

### Workaround
Shutdown all the apps running in the background in your iPhone. Before starting the web server, go on Google Maps to look up the longtitude and latitude of your current location. Set the coordinates in the web interface (You should also change the .gpx files and index.erb to your current location, so that you don't need to do it every time). Run the Debug app and then open your map app (Google Maps for instance) and verify that you can move around via the web interface. Try not to move too far away from your current location during the game as sometimes the OS shuts down the debug app (this happens when the iPhone resources is low, say you are inside a Gym: rendering takes up a lot of resources) and you'll be teleported back to your current location. If you moved too far away, you will risk being banned :)

## Main Components
- a blank iOS project, used in Debug mode for `Simulate Location`
- a web interface made via Sinatra to interact with PokemonGo from [PokemonGoControllerSuite](https://github.com/adin283/PokemonGoControllerSuite/tree/master/PokemonGoController)
- an AppleScript for sending GPS location signals

## System Requirement

- Xcode installed (Obviously you need a Mac, an Apple Developer Account is not needed if you have iOS 9 and above)
- Any iOS device with Pokemon GO installed

## Installation Instructions

### Open foo.xcodeproj

Connect your iOS device and run the project. Remember in to turn simulate location on.
Very important: Debug->Simulate Location->PokemonLocation is checked, otherwise it will not work.

### Start web server

```bash
sudo gem install sinatra #If you are outside of China
sudo gem install sinatra -s http://gems.ruby-china.org #If you are in China
```

Go into the terminal, and run the following

```
./start-web
```

You should see the debug messages below, now in a web browser open http://127.0.0.1:3001

```
== Sinatra (v1.4.7) has taken the stage on 3001 for development with backup from Puma
Puma starting in single mode...
* Version 3.4.0 (ruby 2.3.1-p112), codename: Owl Bowl Brawl
* Min threads: 0, max threads: 16
* Environment: development
* Listening on tcp://localhost:3001
Use Ctrl-C to stop
```

<img width="456" alt="2016-07-13 11 22 11" src="https://cloud.githubusercontent.com/assets/5518/16790893/18843eb2-48ec-11e6-919e-40d9cfb3ca74.png">

You can now interact with the webpage and the AppleScript will transmit the new GPS signal to the iOS device. Now feel free to relax and play the game without moving your legs.

Clicking in the web browser on the computer can be a bit of a pain. Mainly because it triggers Xcode to popup every time a move is made. Instead, find out the local ip of your Mac. Then, go to the hosted server port via Safari or Chrome from another iPhone or iPad to use it as a remote, the address will be something like 192.168.1.x:3001.

### Crowdsourced Maps that Help You Catch all Pokemons:
Having trouble finding new pokemons? Try looking up the following map tools to find the pokemon you are looking for!
- [Pokecrew - Around the World] (http://www.pokecrew.com/?latitude=37.38870308649053&longitude=-122.08420737304687&zoom=14)
- [Pokemapper - Around the World] (https://pokemapper.co/)
- [Gotta Catch'em All - Boston] (https://www.google.com/maps/d/viewer?mid=1mA00u2SuvuNtGCifo0E-BVzTTWc)
- [Pokemon Go Washington - Seattle Area] (https://www.google.com/maps/d/viewer?mid=136ZOge0QKEGZpWMqa9XGe_iyu6Y)

### Screencaps

<img width="1096" alt="2016-07-13 11 22 56" src="https://cloud.githubusercontent.com/assets/5518/16790900/2f3dc9f2-48ec-11e6-85eb-c2efa52699a7.png">

<img width="1072" alt="2016-07-13 11 24 07" src="https://cloud.githubusercontent.com/assets/5518/16790916/54f0d2e8-48ec-11e6-9efc-c8d9f495a76d.png">

<img width="480" src="https://ruby-china-files.b0.upaiyun.com/photo/2016/85aa2df3ded3d77143308f05a0809939.jpg!large" />

### References:

- https://ruby-china.org/topics/30510
