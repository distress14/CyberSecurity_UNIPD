Find the exe file, and use ```string``` command. It will let us to view all of the strings inside the executable

But first, you need Xcode and the Xcode Developer Tools, which comes already with the Xcode App

II. You need to ```cd``` to the exec file directory
```
cd /Path/to/the/CTF_Challenge/exemple_Reykjavik
```

Then type ```strings [Exe_File_Name]``` 
```
strings Reykjavik
```

TO EXPLORE/TO ADD what .strings does °°°°°°°°°°°°°°°°°°°°°

III. Type ```otool -tvV [Exe_File_Name]```
```
otool -tvV Reykjavik
```
If there's no errors, It will give you every method that the program uses

IV. You can search for a particularly function by typing this
```
otool -tvV Reykjavik | grep "method_name"
```

You need to copy the [method name stored in the executable], the one that starts with __ (double)

You need to copy it without the first _

And run it on a debugger
```
lldb [Exe_File_Name]
```

And then
```
disassemble -b -n main     //Disassemble the main function
```

Run it on the specific function
```
disassemble -b -n [_method name stored in the executable_]
```

Copy the address?? of your interest

Open the path and drag the Exe File into the Hex Editor
		Hex Editor: https://hexfiend.com

After that, go to Find, and Find again

Paste the Hex you found in the find field and your goal on the replace field

Then save it

Hopper can do in a simple way, but It costs money.
https://www.hopperapp.com. [99$ personal License]


## Decompiler Explorer

https://dogbolt.org
https://github.com/decompiler-explorer/decompiler-explorer

You can check here how different decompliers works

Source: https://www.youtube.com/watch?v=-r2JXRFU9xE
