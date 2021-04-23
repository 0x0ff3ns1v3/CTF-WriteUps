# Inspector Gadget
![[Pasted image 20210423175055.png]]

This challenge wants us to check the files for the flag. We can recursively download all files to grep for interesting strings.
```bash
└──╼ $wget -r 178.62.14.240:32044
```
 If we grep for the chars ``` _ { }``` we can find the flag pieces within the file.
 ```bash
──╼ $grep -RE "_|CHTB{|\w+}" *
178.62.14.240:32044/index.html:      <center><h1>CHTB{</h1></center>
178.62.14.240:32044/index.html:   <!--1nsp3ction_-->
...snip...
178.62.14.240:32044/static/css/main.css:/* c4n_r3ve4l_ */
...snip...
178.62.14.240:32044/static/js/main.js:console.log("us3full_1nf0rm4tion}");)
...snip...
```
