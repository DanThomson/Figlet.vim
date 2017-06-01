# Figlet

### tl;dr:
* Same license as Vim
* Use the g@ operator or the :Figlet command to filter your text through figlet, in-place!
* :Figlet has a completion function that will complete on installed font names, too.
* Easy, Right? But first you have to have a figlet command line command installed


#### Debian like distributions:
```shell
apt-get install figlet
```

#### Apple Mac OS X:
* Homebrew:
```shell
brew install figlet
```


### ntl;wr! ~~not that long; will read!~~

#### Derived from: [http://www.vim.org/scripts/script.php?script_id=3359](http://www.vim.org/scripts/script.php?script_id=3359)
#### Original README:

* Use the g@ operator or the :Figlet command to filter your text through figlet, in-place!
* :Figlet has a completion function that will complete on installed font names, too.
* Plus, there is a Windows/MS-DOS version of Figlet, so everybody can get in on the fun!

- Q: Can't I do this same thing with the :! command?
- A: Basically, sure

- Q: What does this plugin give me that Vim's built-in filtering doesn't?
- A1. Convenience - through variables it can remember your defaults
- A2. Completion - so you don't have to memorize all of the commands or font names
- A3. Text-objects - use the g@ operator with text-objects for blazing fast transformations that will knock shoulder-surfer's socks off
- A4. A font sample buffer to help you pick out the perfect font for the occasion

- Q: Okay, I'm sold.  But what is this Figlet you speak of?
- A: This:
```shell
  __ _       _      _   
 / _(_) __ _| | ___| |_ 
| |_| |/ _` | |/ _ \ __|
|  _| | (_| | |  __/ |_ 
|_| |_|\__, |_|\___|\__|
       |___/            
```

Er, that wasn't quite as impressive as I was hoping.  Check out [figlet.org](http://www.figlet.org/) to get with the times.

#### TODO:
Fix doc/figlet.txt and doc/tags


### Documentation extracted from the source code:
```vimscript
" ==========================================================================
" File:         Figlet.vim (global plugin)
" Last Changed: 2011-06-22
" Maintainer:   Erik Falor <ewfalor@gmail.com>
" Version:      2.0
" License:      Vim License
" Source:		http://www.vim.org/scripts/script.php?script_id=3359
" ==========================================================================

"  _____ _       _      _        _  __        
" |  ___(_) __ _| | ___| |_     (_)/ _|_   _  
" | |_  | |/ _` | |/ _ \ __|____| | |_| | | | 
" |  _| | | (_| | |  __/ ||_____| |  _| |_| | 
" |_|   |_|\__, |_|\___|\__|    |_|_|  \__, | 
"          |___/                       |___/  
"                ,        ,           , .     , .       
"   . _ . .._.  -+- _ \./-+-  .    ,*-+-|_   -+-|_  _   
" \_|(_)(_|[     | (/,/'\ |    \/\/ | | [ )   | [ )(/,  
" ._|                                                   
"                          @@@@@@@@@          
"                        @@:::::::::@@        
"                      @@:::::::::::::@@      
"    ggggggggg   ggggg@:::::::@@@:::::::@     
"   g:::::::::ggg::::g@::::::@   @::::::@     
"  g:::::::::::::::::g@:::::@  @@@@:::::@     
" g::::::ggggg::::::gg@:::::@  @::::::::@     
" g:::::g     g:::::g @:::::@  @::::::::@     
" g:::::g     g:::::g @:::::@  @:::::::@@     
" g:::::g     g:::::g @:::::@  @@@@@@@@       
" g::::::g    g:::::g @::::::@                
" g:::::::ggggg:::::g @:::::::@@@@@@@@        
"  g::::::::::::::::g  @@:::::::::::::@       
"   gg::::::::::::::g    @@:::::::::::@       
"     gggggggg::::::g      @@@@@@@@@@@        
"             g:::::g                         
" gggggg      g:::::g                         
" g:::::gg   gg:::::g                         
"  g::::::ggg:::::::g                         
"   gg:::::::::::::g                          
"     ggg::::::ggg                            
"        gggggg                               
"
"                               .-.             
"                              .' `.            
"  .--. .---.  .--. .--.  .--. `. .'.--. .--.   
" ' .; :: .; `' '_.': ..'' .; ; : :' .; :: ..'  
" `.__.': ._.'`.__.':_;  `.__,_;:_;`.__.':_;    
"       : :                                     
"       :_;                                     
"
" o                  |    |o|    o              |             |    |         
" .,---.    ,---.,---|,---|.|--- .,---.,---.    |--- ,---.    |--- |---.,---.
" ||   |    ,---||   ||   |||    ||   ||   |    |    |   |    |    |   ||---'
" ``   '    `---^`---'`---'``---'``---'`   '    `---'`---'    `---'`   '`---'
"
"      ______________        ______    _____ 
" ________  ____/__(_)______ ___  /______  /_
" ___(_)_  /_   __  /__  __ `/_  /_  _ \  __/
" ___  _  __/   _  / _  /_/ /_  / /  __/ /_  
" _(_) /_/      /_/  _\__, / /_/  \___/\__/  
"                    /____/                  
"                                                                 888 
"  e88'888  e88 88e  888 888 8e  888 888 8e   ,"Y88b 888 8e   e88 888 
" d888  '8 d888 888b 888 888 88b 888 888 88b "8" 888 888 88b d888 888 
" Y888   , Y888 888P 888 888 888 888 888 888 ,ee 888 888 888 Y888 888 
"  "88,e8'  "88 88"  888 888 888 888 888 888 "88 888 888 888  "88 888 
" 
" 
"                                   .-._.).--.            
"                       `-=-.`-=-. (   )/      `-=-.`-=-. 
"                                   `-'/                  
"
"                (o)__(o)\\  //                wWw  wWw\\\  ///,
"                (__  __)(o)(o)  wWw     wWw   (O)  (O)((O)(O)) 
"                  (  )  ||  ||  (O)_    (O)_  / )  ( \ | \ ||  
"                   )(   |(__)| .' __)  .' __)/ /    \ \||\\||  
"                  (  )  /.--.\(  _)   (  _)  | \____/ ||| \ |  
"                   )/  -'    `-`.__)   )/    '. `--' .`||  ||  
"                  (                   (        `-..-' (_/  \_) 
"           ___  ___  ___  ____   ________ __  __   __    __ ___ _  _
"           ||\\//|| // \\ || \\ ||   || \\||\ ||   ||    ||// \\\\//
"           || \/ ||((   ))||  ))||== ||_//||\\||   \\ /\ //||=|| )/ 
"           ||    || \\_// ||_// ||___|| \\|| \||    \V/\V/ || ||//  
"                          _                     _        
"                        _| |_ ___  ._ _ _  ___ | |__ ___ 
"                         | | / . \ | ' ' |<_> || / // ._>
"                         |_| \___/ |_|_|_|<___||_\_\\___.
"                                                            
"                        _    _                _              _ 
"                   ___ | | _| | ___  ___ ___ | |_  ___  ___ | |
"                  / . \| |/ . ||___|<_-</ | '| . |/ . \/ . \| |
"                  \___/|_|\___|     /__/\_|_.|_|_|\___/\___/|_|
"                                                               
"               _                                       _            
"              (_)                                     (_)           
"            _ (_) _  _    _  _  _  _   _         _  _ (_) _  _      
"           (_)(_)(_)(_)  (_)(_)(_)(_)_(_) _   _ (_)(_)(_)(_)(_)     
"              (_)       (_) _  _  _ (_)  (_)_(_)      (_)           
"              (_)     _ (_)(_)(_)(_)(_)   _(_)_       (_)     _     
"              (_)_  _(_)(_)_  _  _  _  _ (_) (_) _    (_)_  _(_)    
"                (_)(_)    (_)(_)(_)(_)(_)       (_)     (_)(_)      
"                                                                    
"                                                                    
"                _  _   _     _  _                                    
"              _(_)(_) (_)   (_)(_)                                   
"           _ (_) _  _  _       (_)    _  _  _  _      _  _  _  _     
"          (_)(_)(_)(_)(_)      (_)   (_)(_)(_)(_)_  _(_)(_)(_)(_)    
"             (_)      (_)      (_)  (_) _  _  _ (_)(_)_  _  _  _     
"             (_)      (_)      (_)  (_)(_)(_)(_)(_)  (_)(_)(_)(_)_   
"             (_)    _ (_) _  _ (_) _(_)_  _  _  _     _  _  _  _(_)  
"             (_)   (_)(_)(_)(_)(_)(_) (_)(_)(_)(_)   (_)(_)(_)(_)    
" 
"
" ___  _   _     ____ ____ _ _  _    ____ ____ _    ____ ____    
" |__]  \_/  .   |___ |__/ | |_/     |___ |__| |    |  | |__/    
" |__]   |   .   |___ |  \ | | \_    |    |  | |___ |__| |  \    


" This plugin requires that the fully awesome program `figlet' be installed on
" your system.
"
" If you're on Windows, hope is not lost.  There is a figlet port for MS-DOS
" here: ftp://ftp.figlet.org/pub/figlet/program/ms-dos/figdos22.zip.
" Be sure to specify the font directory in your _vimrc through the
" g:filgetOpts variable.
"
" Figlet for MS-DOS is an old program, so you should make sure that your font
" files conform to FAT-16 style 8.3 filenames, and don't use fancy paths with
" spaces:
"
" let g:figletFontDir = 'C:\PROGRA~1\FIGLET\FONTS'

"     _ ,                                         
"   ,- -               ,                          
"  _||_          _    ||                          
" ' ||    _-_   < \, =||= \\ \\ ,._-_  _-_   _-_,  <>
"   ||   || \\  /-||  ||  || ||  ||   || \\ ||_.     
"   |,   ||/   (( ||  ||  || ||  ||   ||/    ~ ||    
" _-/    \\,/   \/\\  \\, \\/\\  \\,  \\,/  ,-_-   <>
                                                     
"1.	If figlet fails to run, your original text is put back w/o messing up your
"	undo history too much (you can still redo to the oopsie).

"2.	:Figlet command can accept a range, and does completion.  Hit tab after
"	typing the -f switch to list available fonts.
"	Get a lot of fonts at http://www.figlet.org/fontdb.cgi
"
"	Ex. Render lines 1 through 7 in the tengwar font:
"	:1,7Figlet -f tengwar
"

"3.	Width is inferred from your 'textwidth' (except on Windows with the DOS
"	build of figlet, as noted above).

"4.	The :FigletFontDemo command will show you a sample of each font installed
"	in your font directory.  By default this command will render each font
"	eponymously, or you may specify a snippet of text to render so as to allow
"	comparison between fonts.
"
"	Ex. See what the word "Supercalifragilisticexpialidocious" looks like in each font:
"	:FigletFontDemo Supercalifragilisticexpialidocious

"5.	The g@ operator takes all of the chosen text (selected with motion
"	commands or text-objects) and puts it all into the same paragraph.
"	the :Figlet command works one line at a time.  It makes a difference
"	when rendering text like this:
"
"1.
"2.
"
"	:Figlet outputs:
"  _    
" / |   
" | |   
" | |_  
" |_(_) 
"       
"  ____     
" |___ \    
"   __) |   
"  / __/ _  
" |_____(_) 
"           
"	g@ instead outputs:
"  _     ____     
" / |   |___ \    
" | |     __) |   
" | |_   / __/ _  
" |_(_) |_____(_)
"

"  _ _    _ ,                            
" - - /  - -                             
"   ('||  ||          _     _            
"  (( ||--||   _-_,  < \,  / \\  _-_  <> 
"  (( ||--||  ||_.   /-|| || || || \\    
"  (( /   ||   ~ || (( || || || ||/      
"    -___-\\, ,-_-   \/\\ \\_-| \\,/  <> 
"                          /  \          
"                         '----`         

" :Figlet takes the same arguments that the program figlet accepts.  It does a
" little bit of parsing for arguments it can grok, and passes the rest through.
" If no arguments are given, it will fall back to the global parameters you can
" set in your .vimrc, or the defaults.  That usually means the 'standard' font
" and a width of 76 columns.
"
" g@, on the other hand, doesn't take arguments.  You can only control it
" through the globals:
"
" g:figletFont - the name of the font to use
" g:figletFontDir  - full path to the directory storing your figlet fonts
" g:figletOpts - the other arguments you want to pass figlet


" 8""""8                         8""""8                                 
" 8    8   eeee eeeee e  eeeee   8      eeee eeeee  e  eeeee eeeee      
" 8eeee8ee 8    8   8 8  8   8   8eeeee 8  8 8   8  8  8   8   8        
" 88     8 8eee 8e    8e 8e  8       88 8e   8eee8e 8e 8eee8   8e  88   
" 88     8 88   88 "8 88 88  8   e   88 88   88   8 88 88      88       
" 88eeeee8 88ee 88ee8 88 88  8   8eee88 88e8 88   8 88 88      88  88   
"
"eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee 
"eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee eeeee 
```

