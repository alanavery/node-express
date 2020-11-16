### Node Express

## Set Up Your Program

1. Create a new repo, `node-express`, and clone it to your local computer.

2. Initialize Node Package Manager inside of the `node-express` directory.

```
npm init
```

3. Answer the setup prompts. If you want to move forward with a default setting, simply hit `return`.

4. If the initialization was successful, you will see the addition of `package.json` within the `node-express` directory.

5. Create an entry point file named `index.js`.

```
touch index.js
```

6. Run your program.

```
node index.js
```

## Test Drive Your Program

1. Inside `index.js`, add an expression that logs a message to the console.

```js
console.log('Howdy! Alan here.');
```

2. Save the file and run your program. Your message should appear in the terminal.

```
node index.js
Howdy! Alan here.
```

## Set Up an Express App

1. Create a new directory for your app, and initialize Node Package Manager inside of it.

```
mkdir new-directory
npm init
```

2. Install the Express package to your directory.

```
npm i express
```

3. Create an entry point file named `index.js`.

```
touch index.js
```

4. Inside the file, import Express and create an instance of it.

```js
let express = require('express');
let app = express();
```

5. Now you can establish your home route using Express's `get()` and `listen()` methods.

```js
app.get('/', (req, res) => {
  res.send('This is the home route.');
});

app.listen(8000);
```

6. Test your route by visiting [`http://localhost:8000`](`http://localhost:8000`) in your browser. You should see the text "This is the home route."

## Create Additional Routes

1. In addition to your home route, you can create more routes by using the `get()` method with a different URL argument.

```js
app.get('/about', (req, res) => {
  res.send('This is the About page.');
});
```

2. Test new routes by appending the URL argument to `http://localhost:8000`, and visiting the full URL in your browser.

## Send Text to the Client

1. With your routes created, your server can now receive requests and send responses back. One type of response that be can sent is simple text, which is accomplished by using the `send()` method.

```js
res.send('Here is a text response');
```

2. When you use Express's `get()` method, it automatically receives two objects as arguments: one is the request object (`req`) and the other is the response object (`res`). The `send()` method takes a string and attaches it to the response object, which is then sent back to the client.

## Send HTML to the Client

1. Another type of response that can be sent to the client is HTML. This can be accomplished by using the `render()` method.

```js
res.sendFile(__dirname + '/views/index.html');
```

2. Instead of providing a string of text, like you did with `send()`, you provide the absolute path to an HTML file. That file gets attached to the response object and sent back to the client.

3. There are a few things to note about the path you must provide:

- `__dirname` is a Node keyword you can use that automatically provides the path to your current directory.

- Add, or concat, your relative path to the end of `__dirname` to form the absolute path.

- It's good practice to make a directory named `views`, where you can save all of the HTML files your server may send to the client.

## Build Templates with EJS

1. EJS is a handy tool called a template engine, and it's available via the Node Package Manager. Template engines give you the ability to inject values and script logic directly into the HTML you send to the client, allowing for customizable, dynamic content. Before you can take advantage of EJS, you must install it.

```
npm install ejs
```

2. You also need to set the view engine to EJS with Express's `set()` method. Add the following expression to `index.js`, above the routes you created.

```js
app.set('view engine', 'ejs');
```

3. Now that EJS is installed and ready to go, you need to update your routes. First, replace the `.html` at the end of your response files with `.ejs`. Then use the method `render()` instead of `sendFile()`, and replace the absolute path you provided with just the name of the file.

```js
// Old route
app.get('/', (req, res) => {
  res.sendFile(__dirname + '/views/index.html');
});

// New route
app.get('/', (req, res) => {
  res.render('index.ejs');
});
```

4. Once all of your routes have been updated, you can start using them to pass values into your HTML. This is done by passing an object into the render function. Note: the object must have at least one key-value pair.

```js
app.get('/', (req, res) => {
  res.render('index.ejs', { name: 'Alan Avery', age: 36 });
});
```

5. You can now use the data inside that object in your EJS/HTML files. You simply make use of some special tags: `<% %>`. Use these tags alone to embed any JavaScript into your files, or add `=` directly after the first tag to print content to the screen.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Home Page</title>
  </head>
  <body>
    <h1>Welcome. My name is <%= name %> and I'm <%= age %> years old.</h1>
  </body>
</html>
```