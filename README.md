# SVGvisits
Simple SVG counter - a simple hit counter application with a few lines of code.

# Demo: <img src="https://githubviews-adjlhysseu.now.sh/">

# How does this works

In this example i will count the number of hits in my node server, and it's much simpler than you would expect.

There is a <text> element in SVG, so we can show the number of hits using this tag element.
  
So the idea is simple :

1. create a simple web server using node, every request we will increment the variable value, and the GET request returns SVG code

```javascript
var http = require('http');
var counter = 0;
var server = http.createServer(function (req, res) {  
	
	if (req.url == '/') {
		counter++;
		console.log(counter);        
    res.writeHead(200, { 'Content-Type': 'image/svg+xml' });  // SVG MIME type        
    // SVG code with text tag (contains counter)
    res.write(`<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="90" height="20"><linearGradient id="b" x2="0" y2="100%"><stop offset="0" stop-color="#bbb" stop-opacity=".1"/><stop offset="1" stop-opacity=".1"/></linearGradient><clipPath id="a"><rect width="90" height="20" rx="3" fill="#fff"/></clipPath><g clip-path="url(#a)"><path fill="#555" d="M0 0h39v20H0z"/><path fill="#e05d44" d="M39 0h51v20H39z"/><path fill="url(#b)" d="M0 0h90v20H0z"/></g><g fill="#fff" text-anchor="middle" font-family="DejaVu Sans,Verdana,Geneva,sans-serif" font-size="110"> <text x="205" y="150" fill="#010101" fill-opacity=".3" transform="scale(.1)" textLength="290">visits</text><text x="205" y="140" transform="scale(.1)" textLength="290">visits</text><text x="635" y="150" fill="#010101" fill-opacity=".3" transform="scale(.1)" textLength="${counter.toString().length * 68}">${counter}</text><text x="635" y="140" transform="scale(.1)" textLength="${counter.toString().length * 68}">${counter}</text></g> </svg>`);
        res.end();
    }
	
});

server.listen(5000); 
console.log('Node.js web server at port 5000 is running..')

```

2. we will Deploy our app in the server, in my case i'm using "now.sh". After you will get the server URL

3. In your markdown, use the server URL with <img> tag in markdown. In our example :

`<img src="https://YOUR_URL_HERE/">`

Done! you have now a visitor Counter.

Hope you like it
