###mnds Multicast DNS
<!--
[![Tests](http://img.shields.io/travis/soef/soef/master.svg)](https://travis-ci.org/soef/soef)
[![Build status](https://ci.appveyor.com/api/projects/status/njb3gh6f49motmuk?svg=true)](https://ci.appveyor.com/project/soef/soef)
-->
[![NPM version](http://img.shields.io/npm/v/mdns-discovery.svg)](https://www.npmjs.com/package/mdns-discovery)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](https://github.com/soef/soef/blob/master/LICENSE)


####Some Examples:

Find all Amazon Fire TV devices on the local network:
```js
var Mdns = require('mdns-discovery');

var mdns = new Mdns({ timeout: 5, name: '_amzn-wplay._tcp.local', find: 'amzn.dmgr:'});
mdns.run (function(res) {
    res.forEach(enry) {
       console.log(entry);
    }
});
```

List all mdns questions and answers for 10 seconds:
```js
var Mdns = require('mdns-discovery');

var mdns = new Mdns({ timeout: 10 });
mdns.on('packet', function (packets, rinfo) {
    if (packets.answers) packets.answers.forEach(function(packet, i) {
        console.log(`A: ${rinfo.address} - packet[${i}]=${packet.name}, type=${packet.type}, class=${packet.class}, ttl=${packet.ttl}}`);
    });
    if (packets.questions) packets.questions.forEach(function(packet, i) {
        console.log(`Q: ${rinfo.address} - packet[${i}]=${packet.name}, type=${packet.type}, class=${packet.class}, ttl=${packet.ttl}}`);
    });
});
mdns.run ();
```

Presence:
```js
var mdns = require('mdns-discovery')();

mdns.onIP('192.168.1.31', function (packet, rinfo) {
    if (packet.answers.length) {
        console.log(rinfo.address + ' is present');
    }
}).run ();
```
