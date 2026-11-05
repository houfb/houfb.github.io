
## JSIntelliSense
A native javascript intellisense tip extension,
for `//...` or `///...` or `////...` or `/*...*/` or `/**...*/` are all can be tip content, 
for `///lib: C:\...\jquery\jquery.js`  or `///lib: ^C:\[\w\-]+\jquery\jquery.js$`  or `/// <reference path="lib/jquery.js" />`  or `import ... from "./jquary.js"`  are all can refer to doc source, the `...`  is same to regular `.+` and `^...$` is treated as regular,
for more to https://houfb.github.io/ .  

!["screenshot"](https://houfb.github.io/softcuts/JSIntelliSense_1.jpg) 


## 🧭 Guide
### How to add comments and references ?

For `//...` or `///...` or `////...` or `/*...*/` or `/**...*/` are all can be tip content, but you can disable some of them in the options dialog. 

For `///lib: C:\...\jquery.js` or `///lib: ^C:\[\w\-]+\jquery.js$`  or `/// <reference path="lib/jquery.js" />` or `import ... from "./jquary.js"` are all can refer to doc source, the `...` in path is same to regular `.+`, and the `^...$` in path is treated as regular, by this way, you can use a simpler way to search the path in your disk.
  
For `common['fn']=...` and `Object.defineProperty(...)` and more complex write way, support a fallback way, you can write a comment left of it, and end with a char `;`, like below :
``` js
//here is a comment for common.fn .
//this is a fallback way to add a comment to any object member.
common.fn;
```

The write way `///lib: ...` is most simple way to add reference, and you can add it to anywhere in your js file, and it will be resolved and collected with the written order, and then, as you can see above img, the multiple comment contents were shown in orderd.  

 

### About regular expression for path ?  
There is four way to write a regular expression to match a file path, by this way, you can get a simple generic way to reference your doc library, which may be relocated to another dir at any time. 

The `^...$` in `///lib: ^.+\jquery.js$` is a standard regular expression, it must be start with `^` and end with `$`, this is the fallback way for a complex regular expression.

The `...` in `///lib: C:\...\jquery.js` is just a simple way to write a regular expression, it will be convert to `.+` internally, and wrapped with `^...$` to match the whole path, and so, it is exactly same as `^...$` , but once you use a regular sensitive char in your path, it may failed, but the char in `:.+-#=[]{}()` were especially processed and it means you can use them in your path directly.

The `**` in `///lib: C:\**\jquery.js` is same as `.*` .

The `*` in `///lib: C:\*\jquery.js` is same as `[^/\\]*` .

> 🧠 Why use `///lib: ...\jquery.js` ?  
> Consider this: you often change the JS doc library path, or in a multi-developer team, you cannot require everyone to use the same JS doc library path, especially when doc are not in the same project and relative path can not be used, however, `/// <reference path="lib/jquery.js" />` require you to do so, therefore, like `///lib: ...\jquery.js`, it is just allow you give a tip and then to auto search the file in your disk.

### About path scheme support ?
The path supported `HTTP|FTP|FILE|UNC|Drive`, the `Drive` is windows drive path like `C:\temp\site.js`, `UNC` is like `\\127.0.0.1\share\site.js`, `FILE` is like `file:///c:\temp\site.js`, above is primary support which is called local file, the `HTTP|HTTPS|FTP|FTPS` is extra extension support which is called remote file, but the remote file can not be cached, and not be tested deeply. 

 

 
## ⚙️ Options 
Open the VS options dialog, and find the `JSIntelliSense` node, you can config the extension here. some of the options need to restart VS.

- ExtNames: the extension names, default is `.js|.ts|.html|.htm|.cshtml|.aspx|.vue|.jsx|.tsx|.md`, you can add more if you want. at you open a file fist with these extensions, the extension will be activated, and then, only the file in these extensions will be resolve and collect terms.
- Modes: some custom setting switches, when multiple, use any of ,;| separate, example: `1|2|4` , need restart vs to clear cache. enum values: 1 = tip list order desc; 2 = `//...` only is not comment; 3 = `///...` only is not comment; 4 = `////...` and more is not comment; 5 = `/*...*/` only is not comment; 6 = `/**...*/` only is not comment; 7 = extra distinct by comment content before reverse.
- SitePath: the real path of the special url \"site.js\", in which you can reference to some static js files that you often use for yourself. when start ^ and end with $ , treated as a regular expression.
- WorkInterval: the interval in seconds between the two resolve works, the first work starts after you open file first in vs.
- MaxCacheCount: the max count to be hold of global cache collection item, which are made by resolve service thread. It will be clear at vs restart.


> 🧠 Why use `SitePath` ?  
> Consider this: most of developer is works in a focused scope in a long time generally, may across multipe project, but use some same docs, and so, a unified refer entry is a good idea, especially in a team, the different across a team is everyone places these docs in different directories, so, instead of scanning every file from disk to use this unified file, it will consume less I/O and CPU. 
 

## 📜 Update Log 
➤ **Version 2.0.0.3**
- Fixed tip content be shown repeatedly in HTML &lt;script&gt;.
- Fixed the comment be errored to stick the keywords above.
- Added a fallback way to add a comment to object member to resolve any complex write way.
 
➤ **Version 2.0.0.2**
- Improved performance via use file path map cache.
- Improved performance via extract left root dir from regular expression to lock to scanning destination dir.
 
➤ **Version 2.0.0.1**
- Fixed tip content not showing issue in HTML &lt;script&gt;.

➤ **Version 2.0.0.0**
- Complete rewrite for VS2022 and next versions.
- Removed sync code, now all is async.  