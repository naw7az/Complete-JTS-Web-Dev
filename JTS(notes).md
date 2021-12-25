# Section: SSH(Secure SHell) ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

**There are 3 techniques used in SSH :**
Encription is a way to hide/jumble a piece of text which is impossible to read by a third party and a person need to decrypt it before reading.

1. Symmetrical Encryption
Uses 1 secret key for both encrytion(E) and decrytion(D).The secret key is exchanged between client and host using key exchange algorithm. The key is generated for each of the SSH session.

```"Hello" -> Key112(E) -> "E11-32ds" -> Key112(D) -> "Hello"```

2. Asymmetrical Encription
Uses two separate keys for encryption and decryption.
The client and host uses a pair of keys(public and private).
the public key (can only)encrytps the data and only the private key that is linked to the public key can decrytp that data.

Say, A has **pubA** and **priA** as two keys. B has **pubB** and **priB** as two keys. B will share **pubB** to A and A will send the data, **pubB** will encryt it and to decryt the data B will use **priB** and vice versa.

      PubA(encrytps)                             PubB(encrytps)
      A                                          B   
      PriA(decrytps pubA encrytion)              PriB(decrytps pubB encrytion)

3. Hashing
Hasing is a way where the client and host uses the key data to encrytps (**HMAC-Hash Message Authentication Code**). Used it in tazapay api call. the client send data along with the hash and the host uses HMAC the encrypt the client data and key to check whether it matches with the hash client has sent. This is used to check whether the data got changed in between the exchange.

# Section: Performance Part 1 :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

**Recap**
When a client calls a server, the server returns an *HTML* file. then in *HTML* file there is a link to stylesheet(*CSS*) and script(*JS*). the client call the server for stylesheet and script to get the complete website data and actions.

 **Network Latency**
 The time takes for a request to travel from client to server and back.

## Network Performance :

We need to know 1 sentence to improve network performance.*Honey I shrunk the files, The traveling deliveryman.* 

First we need to minimize the size our files to improve our network performance, then we need to decrease the download frequency.

1. Minize Text
You can minimize text(HTML, CSS, JS) files using something like uglifyJS.(you can check here[https://skalman.github.io/UglifyJS-online/]). Now, this is part of build process by using webpack so we don't have to do it manually. 

2. Minimize Images

To minimize images we need to choose the correct file format for our system.

- If you want transparency: use a PNG
  
- If you want animations: use a GIF

- If you want colourful images: use a JPG 
  
- If you want simple icons, logos, and illustrations, use SVGs, can customize using css
  
- Reduce PNG with TinyPNG[https://tinypng.com/]
  
- Reduce JPG with JPEG-optimizer[http://jpeg-optimizer.com/] 
  
- Try to choose simple illustrations over highly detailed photographs 

- Always lower JPEG image quality (30-60%) 
  
- Resize image based on size it will be displayed
   
- Display different sized images for different backgrounds(Media Query). 
  
- Use CDNs like imigx 
  
- Remove image metadata 

## Critical Render Path(CRP) :

The Critical Rendering Path is the sequence of steps the browser goes through to convert the HTML, CSS, and JavaScript into pixels on the screen. Optimizing the critical render path **improves** render performance.

- DOM(Document Object Model) -> CSSOM(CSS Object Model) -> Render Tree -> Layout -> Paint

Read More on CRP: [https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path]

1. Optimizing HTML file

We need to load CSS as soon as possible and JS as late as possible. JS blocks page rendering if it is at the top in HTML file(before CSS). 

-  Load style tag in the <head>
-  Load script tag at the end of <body>

2. Optimizing CSS file

CSS is called render blocking because in order to make Render tree we are waiting for CSS to have CSSOM and combine it with DOM. we should make CSS as small as possible.

- Load only what is needed.
- Above the fold loading(load CSS only for the initial screen first, then load rest of CSS after web page is loaded)
- Media Attributes
- Less Specificity

3. Optimizing JS file

Script file can alter the DOM and the CSSOM, hence JS file in CRP is called Parser Blocking. JS file is executed after DOM and CSSOM is executed and JS file can acccess and alter CSSOM and DOM and then we will get the render tree.

- Load Scripts asynchronously
- Defer Loading of scripts
- Minimize DOM manipulation
- Avoid long running Javascript

With async, the file gets downloaded asynchronously and then executed as soon as it’s downloaded.
With defer, the file gets downloaded asynchronously, but executed only when the document parsing is completed. With defer, scripts will execute in the same order as they are called. 

More on [<script async> vs <script defer>](https://bitsofco.de/async-vs-defer/){:target="_blank"}
