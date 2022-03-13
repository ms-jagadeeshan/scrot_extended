# scrot_extended

## Prerequisite
This program is written for Linux, and it needs `import` and `xdotool` command
```sh
# Debian based distros
sudo apt-get install xdotool
```
And it uses `pillow` and `imagehash` python module
Install it using,
### Using pip
```
pip3 install pillow imagehash
```
###

## Installation
### User install
```bash
# making sure .local/bin exists
mkdir -p ${HOME}/.local/bin
curl -sL "https://raw.githubusercontent.com/ms-jagadeeshan/scrot_extended/main/scrot_extended" -o ${HOME}/.local/bin/scrot_extended
chmod +x ~/.local/bin/scrot_extended
```
### System wide install
```
sudo mkdir -p /usr/local/bin
sudo curl -sL "https://raw.githubusercontent.com/ms-jagadeeshan/scrot_extended/main/scrot_extended" -o /usr/local/bin/scrot_extended
sudo chmod +x /usr/local/bin/scrot_extended
```
### Uninstall
For user install
```
rm ~/.local/bin/scrot_extended
```
For system wide install
```
sudo rm /usr/local/bin/scrot_extended
```
## Configuring
In line [18](./scrot_extended#L18) config ={ ... } is there, you **MUST** change "browser" value to the browser you use, eg. "browser": "firefox". <br>
And you can change other default values like target directory, temporary direcotry, delay time. <br>
Also you can add coordinates in "classcoords" : {....} ,like 
```json
"classcoords": {
        "sample": ["1", "1", "500", "400"],
        "classname1": ["12", "100", "1200", "1000"]
    }
```
So that you don't need to pass coordinates each time,you could directly run
```bash
# This will take screenshot with coordinates as x=12,y=100,w=1200,h=1000
$ scrot_extended --class classname1 
```

## Usage
```
Usage : scrot_extended [-s] [-a x-coord,y-coord,widht,height] [-c classname] [-d delay-time] [-t x1,y1,x2,y2] [--clean] [--help] [--verbose]           
    -a, --autoselect <x,y,w,h>       non-interactively choose a rectangle of x,y,w,h(topleft x, y and width and height)
    -c, --class  <classname>         classname for creating folder and naming the screenshot
    -d, --delay <seconds>            delay time to take screenshot
    -s, --single                     takes single screenshot as sample to see
    -t --two-points <x1,y1,x2,y2>    non-interactively choose a rectangle of x1,y1,x2,y2(top left x,y and bottom right x,y)
    --cutoff <integer>               cutoff value to compare hash of two images,higher the value, higher the difference allowed(default:5)
    --clean                          cleans the temporary directory to store screenshots i.e ~/.scrot_images
    --help                           display this help and exit
    --silent                         no output, all are redirected to log file
    --select-window <window-name>    select window by name    
    --iselect-window                 interactively select window    
    --verbose                        prints more info of execution
    --version                        output version information and exit

Examples:
    Takes screenshot every 4 seconds and saves if different than previous and saves the image in the folder probalility, cutoff=5 andtaking screenshot of rectangle shape, x1,y1 = 100,100 and x2,y2=900,900
    $ scrot_extended --class probability --delay 4 --cutoff 5 -t 100,100,900,900

    Takes screenshot every 5(default) second, and stores in folder 'probability' and if screenshot coordinate defined in config["classcoords"] then uses it,else takes screenshot of entire window.
    Note: If --autoselect or --two-points specified, then it overrides the coordinates in config["classcoords"] of code.
    $ scrot_extended --class probability

    Takes screenshot once, and save it in current folder in the name of scrot_sample_image.png and screenshot coordinate starts with (20,20) upto width of 500 and height of 500 pixels.
    $ scrot --single --autoselect 20,20,500,500

    Searches window by its name given and takes single screenshot and saves in current directory
    $ scrot_extended --select-window firefox --single

    You can select window interactively and takes single screenshot and saves in current directory
    $ scrot_extended --iselect-window --single

    Tips: $ watch -n 1 'xdotool getmouselocation'     - To get mouse location
```
