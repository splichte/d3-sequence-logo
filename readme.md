# Sequence Logo Generation

This project implements sequence logo generation using d3, given input sequence data in list form. [Wikipedia](http://en.wikipedia.org/wiki/Sequence_logo) gives a good overview of sequence logos.

## Usage

Open `index.html` from Chrome/Firefox. Alternatively, visit [](http://samlichtenberg.com/static/sequence_logo).

## Style

We adopted the [Airbnb style guide](https://github.com/airbnb/javascript) for Javascript, and [JSDoc format](http://usejsdoc.org/) for our function comments. The code was run through the [ESLint](http://eslint.org/) JS linter.

## Design decisions

Due to the demo nature of this project, various design decisions were made that may need to be reconsidered if this application were to be deployed in production. I make note of these decisions here. I did not change them in this project because I did not want to prematurely optimize before having an understanding of what type of environments this application would be run in.

### Accepted input data format

This application hardcodes sequence data in the form of a list of strings,for easy processing. In a real application setting, we would probably want to provide a thorough parser for the FASTA format, and provide useful error reporting to the end-user if their data does not conform to our specifications. This kind of thing (input validation) would ideally be performed server-side rather than client-side.

### Size of accepted sequence data

Because this is a demo project, we limited the length and number of sequences in the data that our application allows (see 'index.html'). This is not because the application will break if the sequence data is outside this range, but rather because the quality of visualization will be impacted. For instance, it would be impossible to visualize in a single browser window sequences with length in hundreds or thousands--at that point the visualization would cease to be useful.

How to bound the range of data that this visualization application accepts is not immediate and we may need to investigate usage patterns and end-user needs before deciding on a final solution.

We also placed the restriction that all sequences must be of identical length. If it is desired that sequences may be of varying lengths, this would be an easy change to make.

### Error reporting

Because the application provides its own data, there is very limited error handling. Ideally, all functions which are exposed by `sequence_logo.js` would have their inputs validated and provide useful debugging information.

### Browser and d3 Compatibility

This application was tested on recent versions of Chrome and Firefox. However, there are a vast array of browsers, both desktop and mobile, that this application could be run in. Deciding which browsers to support would probably depend on the end-user constituency--for instance, if many end-users run versions of Internet Explorer, that is something that would need to be considered and it would certainly require more work. At the very least, we would like to send end-users a message to please download a modern current browser to use the application, rather than silently failing.

Further, this project was implemented in the v4 version of d3. If an existing codebase uses v3 or an earlier version, some things would need to be changed to be compatible (for example, d3.scaleLinear() becomes d3.scale.linear()). Most of the capabilities are the same, however.

### Use of local d3 copy

We chose to use a locally hosted copy of d3 instead of pointing to a CDN-distributed version. The disadvantage is speed, because our server may serve this file more slowly. The advantage is predictability: if the CDN goes down or the resource is changed/removed, our application could be unexpectedly impacted. Hosting our own copy prevents this.

### Speed

Little consideration was made to speed, other than to ensure that the computations which run are primarily linear (iterating through the data, etc.) and that the application quickly refreshes on a modern browser in a typical (laptop) end-user environment with modest CPU.

If many end-users run in environments with severely limited computing power or limited network bandwidth, that is something to consider. Options include performance monitoring and tuning (to improve performance once on client side) and minifying the javascript file, using CDNs for distribution, etc. (to improve network latency).

## Improvements that can be made

In addition to the design decisions given above, there are also some technical details for which a better solution may exist.

### Data structure to handle letters more appropriately. 

Currently, the various data around the letters 'G', 'A', 'C', 'T' (the character itself, the SVG path data, the base transforms, etc.) are  kept track of by passing around integer identifiers between various functions. This works fine for a small application, but probably makes the code a bit more difficult to modify if another developer wishes to do that.

## Contact

Contact Sam Lichtenberg (splichte@gmail.com)
