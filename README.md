# pikamee-community-urls
urls to Pikamee's community posts (contain members only)

you will need membership to access the members only posts

I'm using this script to automate the process of saving everything, using the posts.txt with the extention "Save Page WE" on firefox.

This was made for my case, you might need to tweak the script in case you want to use it.
```
#!/bin/bash
filename="Pikamee$(echo $@ | sed "s;/;-;g")"

firefox "https://youtube.com$@"

echo move the cursor to a blank space in the page
xdotool mousemove --screen 0 3800 700

echo scrolls to the bottom of the page
xdotool keydown --delay 120000 End 

echo right click
xdotool click 3 

echo got to the bottom of the options
sleep .5 ; xdotool key End

echo select the extension submenu
sleep .5 ; xdotool key Up

echo enter twice to select it and the next 
sleep .5 ; xdotool key --repeat 2 Enter

echo got to the bottom of the options
sleep .5 ; xdotool key End

echo select "standard items"
sleep .5 ; xdotool key Up

echo confirm it 
xdotool key Enter

echo wait for pop up to show
sleep 60 

echo something will fail to save, confirm it 
xdotool key Enter

echo wait for save prompt to show
sleep 45

echo write the name of the file
xdotool type $filename

echo confirm name
xdotool key Enter

```


and this command to run through the list:
```for item in `cat posts.txt | uniq`; do NAME="$(echo $item | sed 's;/;-;g')"; if ! ls *$NAME* 2> /dev/null; then ./macro.sh $item ; fi  ; done```
