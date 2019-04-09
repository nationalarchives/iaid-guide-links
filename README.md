# IAID / Guide links

A quick proof of concept to surface links between items and research guides. This is based on the data Matt has produced.

## Testing 

A basic service is running on [Heroku](https://mighty-island-64939.herokuapp.com). It can be tested in two ways:
 
 1. Visiting a details page in Discovery and pasting the code below into the JavaScript console for a modern browser (we'd ensure backward compatibility for production, but this is just a demo)

```javascript
fetch(`https://mighty-island-64939.herokuapp.com/${window.location.href.match(/([^/])*$/)[0]}`)
    .then(response => response.json())
    .then(data => {
        console.log(JSON.stringify(data));

        fetch('https://vast-lowlands-86122.herokuapp.com/', {
            method: 'POST',
            mode: 'cors',
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({guides: data})
        })
            .then(response => response.text())
            .then(text => console.log(text))

    })
    .catch(error => console.error(error));
``` 

2. Visiting `https://mighty-island-64939.herokuapp.com/` directly - the base route displays a list of links.