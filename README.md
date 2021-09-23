# electron-kiosk-wayland

A simple Electron Kiosk app that acts as a fullscreen browser
to be used on Ubuntu Core 20 systems with the ubuntu-frame display
server.

## Installing

Install an Ubuntu Core 20 image on your device and configure network
and user, so you can ssh into the system.

First install ubuntu-frame with

    snap install ubuntu-frame
    
Now install this snap with

    snap install electron-kiosk-wayland
    
To quieten log spam please connect the interfaces below

    snap connect electron-kiosk-wayland:hardware-observe
    snap connect electron-kiosk-wayland:process-control
    
## Configuring

  The app comes with a configuarble url option that allows you to 
  pick which page is shown. To use this feature simply call

      snap set electron-kiosk-wayland url=https://www.ubuntu.com
      
  The app will restart with the new URL 
      
## Audio

  To make use of audio playback on your Ubuntu Core 20 Kiosk you
  need to install the pulseaudio snap (currently it requires the version
  from the beta channel, since only this provides the `audio-playback`
  interface

    snap install --beta pulseaudio

  Now connect the app to the audio-playback slot pulseaudio provides

    snap connect electron-kiosk-wayland:audio-playback pulseaudio

  And restart it with

    snap restart electron-kiosk-wayland

  Audio playback should work seamlessly now. To adjust the volume you
  can use the shipped pactl command when logged in via ssh

    sudo pulseaudio.pactl set-sink-volume @DEFAULT_SINK@ +10%

  Raises the volume by 10%

    sudo pulseaudio.pactl set-sink-volume @DEFAULT_SINK@ -10%

  Lowers it by 10%
  To set it to an exact value you use

    sudo pulseaudio.pactl set-sink-volume @DEFAULT_SINK@ 50%

## Building

Just clone this tree, make sure to have `snapcraft` installed, cd into
the cloned tree and just run

    snapcraft
    
This will produce a snap package that you can install with the --dangerous 
option of the ```snap install``` command.

