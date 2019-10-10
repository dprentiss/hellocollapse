"Hello World" for [Collapse OS](https://github.com/hsoft/collapseos) shell
----

These are almost exactly the same instructions as found in the [docs](https://github.com/hsoft/collapseos/blob/master/doc/shell.md). The only difference is that I have supplied the current location of `printstr` in the jump table.

Get the code and build the emulator:
```
git clone https://github.com/hsoft/collapseos.git
cd collapseos
git submodule init
git submodule update
cd tools/emul
make
```

Run the shell:
```
shell/shell
```

You should see this:
```
Initializing filesystem
Collapse OS
>
```

Now you're ready to use the shell. First, use the `mptr` command to point the memory pointer at a new memory location, let's say 0xA000:
```
> mptr a000
A000
>
```

Let's see what's there with the `peek` command:
```
> peek f
000000000000000000000000000000
>
```
This is the first 0x0F bytes of memory begining with 0xA000. Nothing here but post-apocalyptic zeros.

Put your message into memory at 0xA000 with the `poke` command. You tell poke how many characters to expect, 6 in this case, and it will wait for you to type them in. We will type `Hello` (5 characters) followed by Ctrl+@ to send a null character (0x00, our sixth character). Our keystrokes will not echo to the screen:
```
> poke 6
>
```

Now point the memory pointer to the location of `printstr` in the jump table at 0x003F:
```
> mptr 003f
003F
```

Run `printstr` with the `call` command:
```
> call 00 a000
Hello>
```

Congratulations! Now all you need is to rummage through what's left of society for a Z80. Good luck!
