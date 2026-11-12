```sh
echo 'alias fix-cinnamenu="grep -q \"globalThis.__meta\" ~/.local/share/cinnamon/applets/Cinnamenu@json/5.8/applet.js || sed -i \"/function main(metadata/a \    globalThis.__meta = metadata;\" ~/.local/share/cinnamon/applets/Cinnamenu@json/5.8/applet.js && cinnamon --replace &"' >> ~/.bashrc && source ~/.bashrc
```  

Now use `fix-cinnamon` to restart cinnamon automatically.  

