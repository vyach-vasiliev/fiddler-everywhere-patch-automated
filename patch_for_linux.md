## Linux

1. Delete `libfiddler.so`.
2. Go to https://github.com/project-yui/Yui-patch/releases
3. Download `libfiddler.so` and `libopen.so`
4. Move `libfiddler.so` to the root path of fiddler.
5. Move `libopen.so` to `resources/app/out/WebServer`
6. Rename `resources/app/out/WebServer/Fiddler.WebUi` to `resources/app/out/WebServer/Fiddler.WebUi1`
7. Create file `resources/app/out/WebServer/Fiddler.WebUi`

   the content of `Fiddler.WebUi`:
    ```shell
    #!/bin/bash
    export LD_PRELOAD=./libopen.so
    ./Fiddler.WebUi1 $@
    ```
8. Open directory `resources/app/out/WebServer` and execute `chmod +x Fiddler.WebUi`
9. Create file `resources/app/out/WebServer/patch.json`

   the content of `patch.json`:
    ```json
    {
        "ClientApp/dist/main-XXXXXXXX.js": {
            "target": "ClientApp/dist/main-XXXXXXXX.original.js",
            "content": "",
            "cur": 0,
            "start": 0,
            "end": 1
        },
        "../main.js": {
            "target": "../main.original.js",
            "content": "",
            "cur": 0,
            "start": 0,
            "end": 1
        }
    }
    ```
   > [!NOTE]
   > XXXXXXXX is a random letters combination that differs from version to version.


10. Copy `ClientApp/dist/main-XXXXXXXX.js` to `ClientApp/dist/main-XXXXXXXX.original.js`
11. Copy `resources/app/out/main.js` to `resources/app/out/main.original.js`
12. Modify file `main-XXXXXXXX.js` and file `main.js` as instructed below.
13. Copy `server/file` -> `Fiddler/resources/app/out/file`

> [!NOTE]
> You may need to recompile `libfiddler.so` and `libopen.so` by yourself.


# How to modify main.js

## For main.js

1. Open `resources/app/out/main.js` in a text editor
2. Open & copy content of `server/index.js` & append to `resources/app/out/main.js` at the begining.