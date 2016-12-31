# Preparation
In order to create repository, you must have macOS or Linux. We don't support other platforms.  
Sample repository is [here](https://github.com/BlitzModder/BMRepository). When you trouble creating repository, please refer to this sample.  
First, you have to create your own [GitHub](https://github.com) account. After that, create a repository named `BMRepository`.
# Create plist file
## Input necessary information
The mod list shown in BlitzModder is generated from plist file on GitHub repository.  
Refer to [Sample plist file](https://github.com/BlitzModder/BMRepository/blob/master/en.plist).  
![correspond-1](http://subdiox.com/blitzmodder/ja/img/correspond-1.png)
First key corresponds to the category name of the mod, and second to the type name of the mod.  
![correspond-2](http://subdiox.com/blitzmodder/ja/img/correspond-2.png)
Second key also corresponds to the title of the screen next to the first screen, and third to the concrete name.  
Dictionary key has to be set as `Display Name:ID`. At this time, please keep the following rules.

- Each key has to include only one `:`. 0 or more than 1 `:` will cause an error.
- English name of mods should be in `en.plist`, and Japanese one should be in `ja.plist`.
- ID should be consisted of lower-case alphabets, number, and underline. It must not include period.

After creating plist file, execute the following commands.

    git add .
    git commit -m "add plist"
    git remote add origin https://github.com/UserName/BMRepository.git
    git push origin master

At this time, mod list can be shown in BlitzModder. Try to add your user name as a repository in BlitzModder.
If some error occurs or nothing is displayed, something is wrong with the above steps. If you can't solve the problem by yourself, ask [@subdiox](https://twitter.com/subdiox) on Twitter.

## Specify compatible Blitz version or OS (optional)
This step is not required, but you can make difference in contents between iOS version and Android version.  
Also, if you specify the compatible Blitz version, users who install Blitz of other than that version can't see them.  
In order to specify them, you have to set the string corresponds to key of mod as follows:  
`Compatible Blitz Version:Compatible OS Type`  

- `Compatible Blitz Version` must include minor version, for example, `3.4.2`.
- `Compatible OS Type` is a 0-4 characters which include `i` in iOS, `a` in Android, `w` in Windows, `m` in macOS.

If your mod is compatible with Blitz 3.4.2 on iOS, Windows, macOS, this string should be `3.4.2:iwm`.  

# Create Install and Remove directory
After creating `en.plist` and `ja.plist`, make `BMRepository` directory and put them in it.
In `BMRepository` directory, make `Install` directory. In `Install` directory, put a directory that has mod data.  
Rename the directory to `Data`, and this directory has to have the same structure as `Data` directory in Blitz.
In other words, the directory has to be able to be applied if you merge it with the original Data directory.  
Next, archive `Data` directory as zip. There are many ways to archive as zip, but please use zip command.   
Launch Terminal, and execute the following command in `Install` directory.

    zip -r First_ID.Second_ID.Third_ID.zip Data

In the case of `Gfx Mods/Reticle/HUD Type`, the file name of it should be `gfx.reticle.hud.zip`.  
After putting all mods data in `Install` directory, execute the following command in `BMRepository` directory.
  
    git add .
    git commit -m "add mods"
    git push origin master

Next, you have to create removal data. I made a script to automatically generate `Remove` directory from `Install` directory.  
Execute the following commands in `BMRepository` directory.

    git submodule add https://github.com/BlitzModder/BMData Data
    curl -O https://github.com/BlitzModder/BMRepository/raw/master/autogen.sh
    bash autogen.sh
    git add .
    git commit -m "add remove"
    git push origin master

# C
# Modの詳細ページの作成 (オプション)
If you want to, you can add detail webpage of your mods to your BMRepository.  
First, make `Detail` directory. Create `en`, `ja`, `img` directory in Detail directory.
Put the html files of the detail pages of your mods in `en`, `ja` directory.
Put images into `img` directory if you use images in your html. html file names have to be `First_ID.Second_ID.Third_ID.html` like as zip file names.  
For example, in `HUD Type` case, it should be `gfx.reticle.hud.html`.  
After you finish putting all detail page files in it, run the following commands:

    git add .
    git commit -m "add html"
    git push origin master

In order to make detail view available, you need to enable GitHub Pages in your GitHub repository.