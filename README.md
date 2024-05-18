# zrfs-js

> ⚠️ This library is still in development.

A JS library for using ZRFS (Z Remote File System) servers.

This library try to replicate the `node:fs.promises` API. 
Check the Node.js documentation : https://nodejs.org/api/fs.html.

To run a ZRFS server check the C tools/library : https://github.com/kapnak/zrfs-c

## Usage

```js
const zprotocol = require('zprotocol-js');
const zrfs = require('zrfs-js');

(async () => {
    // Get he server public key and a local key pair.
    await zprotocol.ready;
    let server_pk = zprotocol.bs32toBytes('GET THE SERVER PK SOMEHOW');
    let local_kp = zprotocol.generate_kp();
    
    // Connect to the server and get the RFS object.
    let rfs = await zrfs.connect('127.0.0.1', 12345, server_pk, local_kp);
    
    // Use RFS object like 'node:fs.promises' :
    await rfs.writeFile('test.txt', 'Hello world!');
    let file = await rfs.open('test.txt', 'r');
    let content = await file.readFile();
    await file.close();
    
    // Remember to disconnect after finished.
    rfs.disconnect();
})();
```

## Contact

Don't hesitate to contact me :
> Mail : kapnak.mail@gmail.com  
> Discord : kapnak

Monero (XMR) :
```
444DEqjmWnuiiyuzxAPYwdQgcujJU1UYFAomsdS77wRE9ooPLcmEyqsLtNC11C5bMWPif5gcc7o6gMFXvvQQEbVVN6CNnBT
```
