# slash-line-component
An example project that demonstrates how to compile a Svelte component into a umd module for use in a micro architecture.  This project is based on the work done here -> https://github.com/sveltejs/component-template 


# How to compile the slash-line-component
Make sure all of the projects dependencies have been installed `npm run i`.  Then run `npm run build`.  This will compile your Svelte component as a UMD module in the dist directory. 

# How to use the compiled slash-line-component
Once compiled *list/SlashLine.js* can then be copied into your web app and loaded via a script tag. Once loaded the components class will be attached to the window using the name specified in the package.json file as a namespace.  In this case window.SlashLine.

Once the script is loaded you can build an instance of the component like this:
```javascript
new window.SlashLine({
            // initial set of props
            props: {
                baseSlashLine: {avg: .240, obp: .324, slg: .318},
                comparatorSlashLine: {name: 'Randy Poffo', avg: .232, obp: .304, slg: .358 }
            },
            // the target that the slash line component will be attached to.
            target: document.getElementById("slashLine")
        });
```
