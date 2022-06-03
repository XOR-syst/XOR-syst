# Obediant Cat
I started learning about cybersecurity with the most beginner friendly CTF: PicoCTF.
It is intended for high school students, but is appropriate for anyone wanting to start out. I started by trying not to use any hints whatsoever, so if I do use the 
provided hints I will add that here as well. 

The first challenge in the PicoGym is worth only 5 points and introduces you to the webshell and linux environments. Before this, I knew a bit of linux, Python, and basic HTML. 
Opening up the challenge we see a download link. Instead of downloading the link onto my machine I decided to use `wget` on the webshell. Copy the URL, and then type 
`wget URL` once you've logged onto the webshell. Don't forget to use Ctrl+Shift+V while pasting. Otherwise... well you can try it the normal way and see why. 

Webshell says the file named flag was installed. Cool now we can read it with: 

`cat flag`

If you're new to Linux, cat is the command that reads the content of files. The flag should be visible now. 
Once I'm done with the files I like to delete them. `rm flag` should take care of that. 

# Mod 26
This one is assigned the category of cryptography. The problem asks us if we know what ROT13 is. If you haven't heard of this before, ROT13 refers to the 
rotation of each letter in the alphabet by 13. You can use an online ROT13 solver to solve for the flag. Alternatively if you're feeling independent, you can write
out all the letter pairings and solve it by hand. If you do it right, you'll have the flag. 

# Python Wrangling
Python is the nicest programming language out there for beginners and is very useful for quick execution of short programs. So let's do what the problem asks us to do. 
Download the files onto the webshell using `wget`. I tried just reading the flag file first by using `cat` and it turned out to be a bunch of random letters, which means
it is likely encrypted. I downloaded the python script and ran it using `python ende.py`. This gave me an output asking me to either use the extension -e or -d. 

Interesting. Probably stands for encode or decode. I tried both and curiously the password gave me an error. So then I decided to just read what the python script. 
The last few lines look important, because you can see that there is actually another extension that works too! -h. 

Running it with `python ende.py -h` shows us the help menu, which gives us the answer to our problem. We need to decrypt the flag file. So I tried 
`python ende.py -d flag.txt.en` 

Entering the copied password now gives us the decrypted flag. 

# Wave a flag
This one is also under general skills, so it shouldn't be anything crazy. Let's get the file onto our webshell. I tried to execute it using `./warm` and permission was of course denied.
No problem, we can just change the permission by adding `chmod +x warm`. After this it should run and say that we can find out more about it by using the option -h. 

And `./warm -h` should just straight up give us the flag. 

# Information
The last challenge worth 10 points is called information and falls under forensics. This time however, the file is a jpg, so I directly clicked the link to install it
onto my machine. Opening up the image I see a cat sitting on top of a laptop. There is however some code on the screen. Since this challenge is only worth 10 points I
didn't think scala and spark were hints. Since I wasn't sure and didn't want to go down a rabbit hole of apache spark and scala, I decided to look at the hint. 

The hint points us to the metadata of the file. There's many ways to do this, but I downloaded the file onto the webshell and used the linux command `exiftool`. 
From all this information, only two of the strings stick out. The license string and the Current IPTC Digest. I tried to base64 decode the license string and it successfully returned the flag.
The syntax for this would be `echo 'string' | base64 --decode`. Echo is the command that returns the output, it works like 'print'. The straight vertical line is piping
the string into the base64 function. --decode is the option that means, well, to decode a base64 encoded string. 

And that's all for these 5 and 10 pointers! Next we'll do the 15 and 20s. 
