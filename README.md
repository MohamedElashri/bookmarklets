 # Bookmarklets

A collection of useful bookmarklets for various purposes.

## Development Bookmarklets

- **Initial commit**: Navigate to the initial commit of a GitHub repository.
  ```
  javascript:(b=>fetch('https://api.github.com/repos/'+b[1]+'/commits?sha='+(b[2]||'')).then(c=>Promise.all([c.headers.get('link'),c.json()])).then(c=>{if(c[0]){var d=c[0].split(',')[1].split(';')[0].slice(2,-1);return fetch(d).then(e=>e.json())}return c[1]}).then(c=>c.pop().html_url).then(c=>window.location=c))(window.location.pathname.match(/\/([^\/]+\/[^\/]+)(?:\/tree\/([^\/]+))?/));
  ```

- **Stop page edit**: Disable page editing mode.
  ```
  javascript: document.body.contentEditable = 'false';document.designMode = 'off';void 0
  ```

- **Make Page editable**: Enable page editing mode.
  ```
  javascript: document.body.contentEditable = 'true';document.designMode = 'on';void 0
  ```

- **Show Github Commit times**: Replace relative time with actual commit timestamp on GitHub.
  ```
  javascript:(function () { document.querySelectorAll("relative-time").forEach(function (el) { var p = el.parentNode; var t = el.title; var s = document.createElement("span"); s.innerHTML = t; p.removeChild(el); p.appendChild(s); }); })();
  ```

- **Faker**: Generate fake data using Faker.js library.
  ```
  javascript: {   import("https://cdn.skypack.dev/@faker-js/faker").then(({ faker: f }) => {     const objFlat = (obj) => {       obj = { ...obj };       delete obj.faker;       const flattened = {};        Object.keys(obj)         .filter((i) => typeof obj[i] === "function" || objtest(obj[i]))         .forEach((key) => {           const value = obj[key];           if (objtest(value)) {             Object.assign(flattened, objFlat(value));           } else {             flattened[key.toLowerCase()] = value;           }         });        return flattened;     };     function objtest(value) {       return (         typeof value === "object" && value !== null && !Array.isArray(value)       );     }     const faker = objFlat(f);     console.log(faker);     let p = "What would you like to generate? (username, email, avatar, etc)";     let answer;     while (!answer) {       answer = prompt(p);       if (!answer) {         answer = "CANCEL";       } else {         answer = answer.toLowerCase().trim();       }       if (answer !== "CANCEL" && !faker[answer]) {         answer = null;         p = `[Invalid], valid keys are: ${Object.keys(faker)}`;       }     }     if (answer === "CANCEL") {       return alert("Cancelled");     }     Promise.resolve(faker[answer]()).then((a) => prompt("Here you go:", a));   }); }
  ```

- **Syntax Highlighter**: Highlight code syntax using highlight.js library.
  ```
  javascript: (function() {    var colorScheme = 'stackoverflow-light';    var link = document.createElement('link');    link.setAttribute('rel', 'stylesheet');    link.setAttribute('type', 'text/css');    link.setAttribute('href', 'https://rawcdn.githack.com/highlightjs/highlight.js/0c98957206664d2aacd72bbfab4479c216f6da7e/src/styles/' + colorScheme + '.css');    document.getElementsByTagName('head')[0].appendChild(link);    var script = document.createElement('script');    script.setAttribute('type', 'text/javascript');    script.setAttribute('src', 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.1.0/highlight.min.js');    document.getElementsByTagName('head')[0].appendChild(script);    script.addEventListener('load', function() {        var pres = document.querySelectorAll(prompt("Elements to highlight (querySelector)", "pre"));        for (var i = 0; i < pres.length; ++i) {            if (!pres[i].querySelector('code')) {                window.hljs.highlightBlock(pres[i]);            } else {                window.hljs.highlightBlock(pres[i].querySelectorAll('code')[0]);            }        }    })}())
  ```

- **Allow copy/paste**: Enable copy and paste functionality on a webpage.
  ```
  javascript:(function()%7B%22use%20strict%22%3Bvar%20all%3Ddocument.getElementsByTagName(%22*%22)%3Bvar%20i%3Bvar%20max%3Bfor(i%3D0%2Cmax%3Dall.length%3Bi%3Cmax%3Bi%2B%3D1)%7Bif(all%5Bi%5D.onCopy)%7Ball%5Bi%5D.onCopy%3Dnull%3B%7Dif(all%5Bi%5D.onPaste)%7Ball%5Bi%5D.onPaste%3Dnull%3B%7D%7D%7D)()%3B
  ```

## Reading Bookmarklets

- **Remove colors**: Remove background and text colors from a webpage.
  ```
  javascript: (function() {var newSS, styles = '* { background: white ! important; color: black !important } :link, :link * { color: #0000EE%20!important%20}%20:visited,%20:visited%20*%20{%20color:%20#551A8B%20!important%20}';if%20(document.createStyleSheet)%20{document.createStyleSheet(%22javascript:'%22%20+%20styles%20+%20%22'%22);}%20else%20{newSS%20=%20document.createElement('link');newSS.rel%20=%20'stylesheet';newSS.href%20=%20'data:text/css,'%20+%20escape(styles);document.getElementsByTagName(%22head%22)[0].appendChild(newSS);}})();
  ```

- **Split vertically**: Split the current webpage vertically into two frames.
  ```
  javascript:document.write('<HTML><HEAD></HEAD><FRAMESET COLS=\'50%,*\'><FRAME SRC=' + location.href + '><FRAME SRC=' + location.href + '></FRAMESET></HTML>')
  ```

- **Split horizontally**: Split the current webpage horizontally into two frames.
  ```
  javascript:document.write('<HTML><HEAD></HEAD><FRAMESET ROWS=\'50%,*\'><FRAME SRC=' + location.href + '><FRAME SRC=' + location.href + '></FRAMESET></HTML>');document.close();
  ```

- **Kill Sticky**: Remove fixed and sticky positioned elements from a webpage.
  ```
  javascript:(function()%7Bdocument.querySelectorAll(%22body%20*%22).forEach(function(node)%7Bif(%5B%22fixed%22%2C%22sticky%22%5D.includes(getComputedStyle(node).position))%7Bnode.parentNode.removeChild(node)%7D%7D)%3Bdocument.querySelectorAll(%22html%20*%22).forEach(function(node)%7Bvar%20s%3DgetComputedStyle(node)%3Bif(%22hidden%22%3D%3D%3Ds%5B%22overflow%22%5D)%7Bnode.style%5B%22overflow%22%5D%3D%22visible%22%7Dif(%22hidden%22%3D%3D%3Ds%5B%22overflow-x%22%5D)%7Bnode.style%5B%22overflow-x%22%5D%3D%22visible%22%7Dif(%22hidden%22%3D%3D%3Ds%5B%22overflow-y%22%5D)%7Bnode.style%5B%22overflow-y%22%5D%3D%22visible%22%7D%7D)%3Bvar%20htmlNode%3Ddocument.querySelector(%22html%22)%3BhtmlNode.style%5B%22overflow%22%5D%3D%22visible%22%3BhtmlNode.style%5B%22overflow-x%22%5D%3D%22visible%22%3BhtmlNode.style%5B%22overflow-y%22%5D%3D%22visible%22%7D)()%3B%0A
  ```

- **Remove inline JS**: Remove inline JavaScript from a webpage.
  ```
  javascript:(function() {   var scripts = document.getElementsByTagName('script');   for (var i = scripts.length - 1; i >= 0; i--) {     if (!scripts[i].src) {       scripts[i].parentNode.removeChild(scripts[i]);     }   } })();
  ```

- **Enable scrolling**: Enable scrolling on a webpage.
  ```
  javascript:(function(){var e=document.getElementsByTagName('body')[0];e.style.overflow='auto';e.style.height='auto';var s=document.createElement('style');s.type='text/css';s.innerHTML='html,body{overflow:auto !important;height:auto !important;}';document.head.appendChild(s);})();
  ```

- **Scroll to Bottom**: Scroll to the bottom of the webpage.
  ```
  javascript: window.scrollTo(0, document.body.scrollHeight || document.documentElement.scrollHeight);
  ```


## Safari Bookmarklets

These are the essential bookmarklets I use with safari (iOS)

- **Kill Sticky**: The famous kill sticky bookmarklet to remove fixed and sticky elements

```
javascript:(function()%7B(function%20()%20%7Bvar%20i%2C%20elements%20%3D%20document.querySelectorAll('body%20*')%3Bfor%20(i%20%3D%200%3B%20i%20%3C%20elements.length%3B%20i%2B%2B)%20%7Bif%20(getComputedStyle(elements%5Bi%5D).position%20%3D%3D%3D%20'fixed')%20%7Belements%5Bi%5D.parentNode.removeChild(elements%5Bi%5D)%3B%7D%7D%7D)()%7D)()
```

- **Replace font**: Replaces the font on page with a font of your choice 

```
javascript:(function()%20%7B%20%20%20document.querySelectorAll('*').forEach(e%20=%3E%20%7B%20%20%20%20%20if%20(!e.style.fontFamily.includes('monospace'))%20%7B%20%20%20%20%20%20%20e.style.fontFamily%20=%20'sans-serif';%20%20%20%20%20%7D%20else%20%7B%20%20%20%20%20%20%20e.style.fontFamily%20=%20'monospace';%20%20%20%20%20%7D%20%20%20%7D);%20%7D)();
```

- **Inject device max-width** : There still many webpage that will not set max-width for mobile phone era yet 

Looking at you Mansoura university, you did not only suspended and kicked me out but still stuck at the early 2000s

```
javascript:(function()%20%7B%20%20%20document.head.insertAdjacentHTML('beforeend',%20%60%20%20%20%20%20%3Cmeta%20name=%22viewport%22%20content=%22width=device-width%22%20/%3E%20%20%20%20%20%3Cstyle%3E%20%20%20%20%20%20%20body%20%7B%20%20%20%20%20%20%20%20%20/*%20Without%20word-break:%20break-word,%20iOS%20Safari%2016.1%20lets%20%20%20%20%20%20%20%20%20%20*%20very%20long%20words%20e.g.%20URLs%20widen%20the%20page%20*/%20%20%20%20%20%20%20%20%20word-break:%20break-word;%20%20%20%20%20%20%20%20%20%20/*%20Don't%20let%20iOS%20Safari%20enlarge%20the%20font%20size%20when%20the%20phone%20is%20in%20landscape%20mode.%20%20%20%20%20%20%20%20%20%20*%20https://kilianvalkhof.com/2022/css-html/your-css-reset-needs-text-size-adjust-probably/%20%20%20%20%20%20%20%20%20%20*/%20%20%20%20%20%20%20%20%20-webkit-text-size-adjust:%20none;%20%20%20%20%20%20%20%20%20text-size-adjust:%20none;%20%20%20%20%20%20%20%7D%20%20%20%20%20%3C/style%3E%20%20%20%60);%20%7D)();
```

- **Nuke fixed elements** : This will remove all fixed elements which are mostly ads 

```
javascript:(function()%7B(function%20()%20%7Bvar%20i%2C%20elements%20%3D%20document.querySelectorAll('body%20*')%3Bfor%20(i%20%3D%200%3B%20i%20%3C%20elements.length%3B%20i%2B%2B)%20%7Bif%20(getComputedStyle(elements%5Bi%5D).position%20%3D%3D%3D%20'fixed')%20%7Belements%5Bi%5D.parentNode.removeChild(elements%5Bi%5D)%3B%7D%7D%7D)()%7D)()
```

- **Go to referrer** : How the hell I got to this page?

```
javascript:if(!document.referrer)%20alert(%22No%20referrer!%22);%20else%20document.location%20=%20document.referrer;%20void%200
```


