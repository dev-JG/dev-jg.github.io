---
layout: default
title: "js 암호화"
tags: JS
---

js 암호화, 자바단 복호화(base64, url인코딩, xor연산포함)
---------------

<br>

- 자바스크립트

```
//base64인코딩
function base64Encode(str) {
    var enc64List, dec64List;
    
    enc64List = new Array();
    dec64List = new Array();
    var i;
    for (i = 0; i < 26; i++) {
        enc64List[enc64List.length] = String.fromCharCode(65 + i);
    }
    for (i = 0; i < 26; i++) {
        enc64List[enc64List.length] = String.fromCharCode(97 + i);
    }
    for (i = 0; i < 10; i++) {
        enc64List[enc64List.length] = String.fromCharCode(48 + i);
    }
    enc64List[enc64List.length] = "+";
    enc64List[enc64List.length] = "/";
    for (i = 0; i < 128; i++) {
        dec64List[dec64List.length] = -1;
    }
    for (i = 0; i < 64; i++) {
        dec64List[enc64List[i].charCodeAt(0)] = i;
    }
    var c, d, e, end = 0;
    var u, v, w, x;
    var ptr = -1;
    var input = str.split("");
    var output = "";
    while (end == 0) {
        c = (typeof input[++ptr] != "undefined") ? input[ptr].charCodeAt(0)
                : ((end = 1) ? 0 : 0);
        d = (typeof input[++ptr] != "undefined") ? input[ptr].charCodeAt(0)
                : ((end += 1) ? 0 : 0);
        e = (typeof input[++ptr] != "undefined") ? input[ptr].charCodeAt(0)
                : ((end += 1) ? 0 : 0);
        u = enc64List[c >> 2];
        v = enc64List[(0x00000003 & c) << 4 | d >> 4];
        w = enc64List[(0x0000000F & d) << 2 | e >> 6];
        x = enc64List[e & 0x0000003F];
        if (end >= 1) {
            x = "=";
        }
        if (end == 2) {
            w = "=";
        }
        if (end < 3) {
            output += u + v + w + x;
        }
    }
    var formattedOutput = "";
    var lineLength = 76;
    while (output.length > lineLength) {
        formattedOutput += output.substring(0, lineLength) + "\n";
        output = output.substring(lineLength);
    }
    formattedOutput += output;
    formattedOutput.replace('+', '-');
    formattedOutput.replace('/', '_');
    formattedOutput.replace('=', '.');
    
    return formattedOutput;
}

function encryptStringWithXORtoHex(input) {
	var key = '#8825';
    var c = '';
    while (key.length < input.length) {
         key += key;
    }
    
    for(var i=0; i<input.length; i++) {
        var value1 = input[i].charCodeAt(0);
        var value2 = key[i].charCodeAt(0);
        var xorValue = value1 ^ value2;
        var xorValueAsHexString = xorValue.toString("16");
        
        if (xorValueAsHexString.length < 2) {
            xorValueAsHexString = "0" + xorValueAsHexString;
        }
        c += xorValueAsHexString;
    }
    return c;
}
```

- 자바단

```
/**
 * https://stackoverflow.com/questions/33529103/simply-xor-encrypt-in-javascript-and-decrypt-in-java
 * */
private static String decryptStringWithXORFromHex(String input,String key) {
    StringBuilder c = new StringBuilder();
    while (key.length() < input.length()/2) {
        key += key;
    }
    
    for (int i=0;i<input.length();i+=2) {
        String hexValueString = input.substring(i, i+2);
        int value1 = Integer.parseInt(hexValueString, 16);
        int value2 = key.charAt(i/2);

        int xorValue = value1 ^ value2;

        c.append(Character.toString((char) xorValue));

    }
    return c.toString();
}
```