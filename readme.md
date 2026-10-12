# sha2playground
the silly lil website app thing that lets you mess w/ sha-2 hashing algorithms!

note that this must be run in a secure context so `window.crypto.subtle` works

i made it by:
1. making a quick "normal" page (index.html) w/ some bonus css/js for style n functionality ofc
2. manually compressing the whole page (into compression.html) by getting rid of anything and everything i didnt need, down to (hopefully) every unneeded space character
3. doing some url escaping cause # and % both appear in it 💔💔💔

no i did not use a tool for the 'compression,' though i did use a javascript minifier to compare sizes because i was curious n ended up taking a technique from it:
```js
// original
for(let i=0;i<x.length;i++){u+=x[i];if(i%16==15)u+="\n"};

// new (horrible! but smart)
for(let i=0;i<x.length;i++)u+=x[i],i%16==15&&(u+="\n");
```

you can see and use it by pasting this into your addressbar:

```
data:text/html,<style>*{font-family:sans-serif;color:%23ffe}body,div{background:%23112;margin:8rem;display:flex;align-items:center;flex-direction:column}h1{margin-bottom:2rem}option,select,textarea{border:1px solid %23666;border-radius:5px;background:%23338;padding:4px 8px}div{background:%23223;padding:2rem;border-radius:25px;margin:0}span{font-family:monospace}</style><body><h1>SHA-2 Playground</h1><div><textarea id="i"onkeyup="h()"placeholder="Input"></textarea><br><br><select id="a"onchange="h()"><option>SHA-256</option><option>SHA-384</option><option>SHA-512</option></select><br>Output:<br><br><span id="o">(output)</span></div><script>let f=a=>document.getElementById(a),i=f('i'),o=f('o'),a=f('a'),e=new TextEncoder;async function h(){o.innerText=s(new Uint8Array(await crypto.subtle.digest(a.value,e.encode(i.value))).toHex())}function s(x){x=x.split('');let u='';for(let i=0;i<x.length;i++)u+=x[i],i%2516==15&&(u+="\n");return u}</script></body>
```


