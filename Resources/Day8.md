##  Upload File module without any libraries


In `server.js` file write 

```
const http = require("http");
const fs = require("fs")
const httpServer = http.createServer();
httpServer.on("listening", () => console.log("Listening..."));
httpServer.on("request", (req, res) => {

    if (req.url === "/") {
        res.end(fs.readFileSync("index.html"));
        return;
    }
//idempotency
    if (req.url === "/upload") {
        const fileName = req.headers["file-name"];
        req.on("data", chunk => {
            fs.appendFileSync(fileName, chunk)
            console.log(`received chunk! ${chunk.length}`)
        })
        res.end("uploaded!")
    }
})

httpServer.listen(3000)

```

In `index.html` write 

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>File uploader</title>
</head>
<body>
    <h1>My file uploader</h1>
     <label for="f">Upload File</label>
     <input type ='file' bname='f' id = 'f'>
    <button id = 'btnUpload'>Read & Upload</button>
    <div id = 'divOutput'>

    </div>

    <script>
        const btnUpload = document.getElementById("btnUpload");
        const divOutput = document.getElementById("divOutput");
        const f = document.getElementById("f");

        btnUpload.addEventListener("click", () => {

            const fileReader = new FileReader();
            const theFile = f.files[0];
            fileReader.onload = async ev => {

                const CHUNK_SIZE = 5000;
                const chunkCount = ev.target.result.byteLength/CHUNK_SIZE;
                 
                console.log("Read successfully");
                const fileName = Math.random() * 1000 + theFile.name;
                for (let chunkId = 0; chunkId < chunkCount + 1; chunkId ++ )
                {
                    const chunk = ev.target.result.slice(chunkId * CHUNK_SIZE, chunkId * CHUNK_SIZE + CHUNK_SIZE );
                    await fetch ("http://localhost:3000/upload", {
                        "method": "POST",
                        "headers": {
                            "content-type": "application/octet-stream",
                            "content-length": chunk.length,
                            "file-name": fileName
                        },
                        "body": chunk
                    })
                    divOutput.textContent = Math.round(chunkId * 100/chunkCount,0) + "%"

                }
                console.log(ev.target.result.byteLength);
            }
            fileReader.readAsArrayBuffer(theFile); 
        })

    </script>
</body>
</html>
```

Now in terminal run `npm start`

Our local server starts at port https://localhost:3000

Go to https://localhost:3000 and see the frontend response and try uploading a file.

See the Console for backend response .


Boom !! You Completed Day 8 Challenge.

[Back to Home](../README.md)