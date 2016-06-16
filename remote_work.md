# Remote Work Guide

How we do remote work in Reevoo.

## Software

- [Zoom](https://zoom.us/) for tele/videoconferencing.
- [Slack](https://slack.com/) for group and private chat
- [Skype](http://www.skype.com) for tele/videoconferencing.
- [Floobits](http://www.floobits.com) for remote pairing

## Zoom

Zoom is Reevoo's proffered videoconferencing software. Everyone should have a zoom account either Pro or Basic, Basic accounts are limited to hosting 30 minute meetings.
The instructions for downloading and setting up Zoom with the Reevoo account are [here](https://reevoo.atlassian.net/wiki/display/PROC/Zoom+Rooms+Instructions).
Everyone should have the client installed and know their username and password to save faffing around at the start of meetings.
When there is a meeting, just log onto the zoom client and wait for an invite from whoever is hosting.

### Floobits

Floobits allows you to share editor, terminal, camera and screen (in whatever combination).
It proved to be fastest and most flexible tool for remote pairing on the current market.
Only one paying user is needed to create a private workspace, other collaborators can use the free account.

#### Setup

1. Sing up on the https://floobits.com/
2. Follow the instructions on https://floobits.com/help/plugins to install Floobits plugin into your favorite
editor (Sublime, IDEA, Neovim or Emacs).
3. Make sure that ~/.floorc.json contains your authentication keys as described on https://floobits.com/help/floorc.
4. You can also install https://floobits.com/help/flootty if you want to share your terminal.

#### Create workspace (with Sublime)stre

1. Open your project in Sublime
2. In the sidebar right-click on the project root folder and select Floobits > Share this (Private)
3. Confirm the workspace url in the input field and press enter
4. Open the workspace url in the browser
5. From the top menu select Collaborate > Workspace permissions
6. Add collaborators using their Floobits account names
7. If you want to share your terminal open it and enter `flootty --url https://floobits.com/owner/workspace_name --create example_terminal_name` (change the workspace url and name of your terminal)

#### Join workspace (with web editor)

1. Just open the workspace url in browser
2. From top menu select Collaborate > Follow changes
3. Click on your avatar in the right sidebar to start the video

#### Join workspace (with Sublime)

1. In Sublime open the Command Palette (cmd+shift+P) and select Floobits - Join Workspace
2. Type the workspace url into input field and press enter
3. If the dialog about conflicted files appear you should in most cases select option Override local changes (unless you really want to override remote changes)
4. open the Command Palette (cmd+shift+P) and select Floobits - Follow Workspace Changes


#### Known Issues

- Changes in files are sometimes not visible outside of the editor for the user who joined the workspace.
So any commands in the terminal (running server, test...) should be run by user who created the workspace.



## Good Practices

### Calling

- Use external microphone when calling by Zoom whenever there are more than two people on the call.
- Check in the Zoom settings whether the connected microphone is actually used.
- Just one person should speek at the same time.
- Distance between the microphone and person speaking shouldn't be more that 2 meters. If it's possible place the mic
in the middle of meeting place.


### Remote Pairing

- Video transmission in Floobits is currently flaky, we've decided to use Skype for this purpose along with Floobits.
