## Display system configuration & specs

In `server.js` file write 

```
const os = require('os')

const info = {
    "Operating System" : os.version(),
    Platform : os.platform(),
    Type: os.type(),
    Architecture: os.arch(),
    "Temp Directory": os.tmpdir(),
    UserName: os.userInfo().username,
    Hostname: os.hostname(),
    "Home Directory":os.userInfo().homedir,
    "Total Memory": (os.totalmem() / 1024 ** 3).toFixed(2) + " GB",
    "CPU Model": os.cpus()[0].model.trimEnd(),
    "CPU Speed":(os.cpus()[0].speed / 1000).toFixed(2) + " GHz"
};

console.table(info)

```

Now in terminal run `npm start`

See the Console response .

# Example Response : 

| (index)  | Values |
|:-----:|:-----------:|
| Operating System | 'Windows 10 Home Single Language' |
| Platform | 'win32' |
| Type     | 'Windows_NT' |
| Architecture  |  'x64' |
|  Temp Directory  | 'C:\\Users\\SUDHAN~1\\AppData\\Local\\Temp' |
|    UserName     |   'Sudhanshu Ranjan'  |
|     Hostname   |   'MSI'  |
|  Home Directory  | 'C:\\Users\\Sudhanshu Ranjan'|
|   Total Memory   |    '7.85 GB' |
|  CPU Model | 'Intel(R) Core(TM) i5-9300H CPU @ 2.40GHz' |
|  CPU Speed     |                '2.40 GHz' |



Boom !! You Completed Day 4 Challenge.

[Back to Home](../README.md)