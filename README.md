# reverse_engeneer
Reverse engeenering 3 crackme's

## 1stcrackme

Reverse engeneering the first crackme was somekind easy i just used radare2 to read the machine code, but first let's give executable permissins to our crackme's
```
$ sudo chmod +x 1stcrackme
$ sudo chmod +x 2ndcrackme
$ sudo chmod +x 3rdcrackme
```
Then open the 1stcrackme:
![](/img/img1.png)
As shown below we need a password for this one, i used this command to open this crackme with radare:
```
r2 1stcrackme
```
Then i pressed 'V' and pressed enter, i scrolled up a bit and found this:
![](/img/img2.png)
The password was `FEDORAGCIPASSEASY` as shown in this image showing the execution:
![](/img/img3.png)
> Password= `FEDORAGCIPASSEASY` stage cleared
## 2ndcrackme
This one was also a walk in the park, i used the `GDb` program you can find the steps i followed in [this](https://asciinema.org/a/aUS6D9Mlq6dbGvpTLC7n1gb1l) asciinema,
When running the program you see this: <br>
![](/img/img4.png)
![](/img/img5.png)  <br>
The little trick here was just that we had to give command line arguments and everything would go well...
> Password=`FEd0raGCIt@sk` stage cleared
### 3rdcrackme (Boss level)
This one really trolled me, it litterally trolled the hell out of me, if i count the number of possible passwords it would amount to 3 or 4, first let's use `strings`:
![](/img/img6.png)  <br>
Easy peasy right??:  <br>
![](/img/img7.png)   <br>
Whut?? why didn't it work,hmm... let's try another method, on this one i'll use GDB and follow the steps shown in the 2 below screenshots:  <br>
![](/img/img8.png) <br>
![](/img/img9.png) <br>
Yeah!!!, found it on memcmp breakpoint now let's try it: <br>
![](/img/img10.png)   <br>
Wrong again??? I had to give up my pride and ask for help in the fedora codein telegram group and a user told me to try out Ghidra, which i immediately installed and tried out, if you know what i'm talking about you don't need a writeup on how to install or do basic stuff with it, I then used ghidra to analyze the file, i got an output like this one:
![](/img/img11.png)
After hours of googling i found a pretty funny thing to exploit the program, when i give memcmp a very large data as input, it will return each time 0,
I tried it and then:
![](/img/img12png)
> Password= `any large input to overflow the stack`
### Conclusion
Reverse engeneering the 1st and second crackme was pretty easy when using some basic linux tools. 
So, for the 3rdcrackme i know i should have extacted the password but the thing was to exploit it so the overflow can be considered as a valid password because when given as input it grants you access to the program
When i was disassembling the 3rdcrackme i found out there was a secret function but with my current knowledge of assembly i could not find a way to exploit it, just can you please tell me what it is after the contest ends??
a little list of false passwords i found on 3rdcrackme: 00g61@k001and1514cel,FEDORAPASSWORDGCI,00g61@k0H,0land151H,4celf 
### References:
I used these video from live overflow as a reference when i was doing the task:
[1](https://www.youtube.com/watch?v=VroEiMOJPm8&list=PLhixgUqwRTjxglIswKp9mpkfPNfHkzyeN&index=7&t=0s)
[2](https://www.youtube.com/watch?v=3NTXFUxcKPc&list=PLhixgUqwRTjxglIswKp9mpkfPNfHkzyeN&index=8&t=0s)
> Password= `any large input to overflow the stack`

Checkout [this](https://asciinema.org/a/aUS6D9Mlq6dbGvpTLC7n1gb1l) asciinema if you want to see the execution of these exploits.


Made by `Shadowblade` During `GCI 2019`, Open source project
