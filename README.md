![Banner](https://github.com/nvsriram/quine/assets/50625504/4faae768-d078-49a4-a70e-5143a0907786)

[From Wikipedia](https://en.wikipedia.org/wiki/Quine_(computing)): A quine is a computer program which takes no input and produces a copy of its own source code as its only output. The standard terms for these programs in the computability theory and computer science literature are "self-replicating programs", "self-reproducing programs", and "self-copying programs".

## ✨ Inspiration

Quines are a very interesting concept and can be extended to take the form of anything from basic console print statements to ASCII art to rotating globes! A simple search on the web will lead you to quite a few exciting quines in almost any programming language <br/>
I was messing around with `three.js` code recently and didn't see any cool 3D HTML based quines so I figured I'd take up the challenge and make my own quine!

## 💭 Things to consider

While making an HTML quine there were two main things I needed to establish:
* **Encoding/Decoding Method**: The underlying code has characters like `'` and `"` that would normally need to be escaped by the language. To go around this, I used _Base-64_ encoding as that can easily encode and decode these characters
* **Output Format**: Most quines online take the form of displaying the underlying code either via the console or as text displayed on the page. I took the route by displaying the underlying code in a rotating sphere generated using `three.js` with a canvas as its texture ;)


## 💻 Implementation

* My quine is in HTML but the real code logic lies in the Javascript script
* I use _Base-64_ for encoding/decoding the underlying code
* The Javascript script can be divided into two sections:
  - The pre-hash (`p`) and the post-hash (`e`)
  - The pre-hash is the _Base-64_ hash of the `<body>` and `<script>` tags before the actual Javascript script
  - The post-hash is the _Base-64_ hash of the Javascript code that contains the real logic until the final closing `</script>` tag
* The code first initializes an empty array `a` that would contain separate <i title="separated by \n">lines</i> which would be used to populate the canvas that is applied as a texture map on the mesh around the `three.js` sphere that you can see rotating in the [demo](#demo)!
* `a` is populated with the decoded pre-hash lines, pre-hash lines as is, post-hash lines as is, and finally the decoded post-hash lines
* After `a` is fully populated, we generate a `<canvas>` element and `fillText` the characters in the lines in `a` while adding appropriate offset, background color, and font colors
* We then create a `three.js` Sphere and attach the canvas to the texture that is mapped to the mesh on top of the sphere
* We set the mesh's initial position and set an interval so that the mesh rotates every `50` milliseconds

## 🚀 Demo

Here you can see the sphere rotating with the underlying code used to generate it displayed on its surface: <br />
![HTML quine GIF](https://github.com/nvsriram/quine/blob/main/quine.gif?raw=true) <br />
You can verify for yourself that the underlying source code and the text displayed on the sphere are identical!

Feel free to clone the project and open the `quine.html` file on a browser to see it run for yourself
