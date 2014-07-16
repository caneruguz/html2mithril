html2mithril
==========

This is a small library that is intended to be used with gulp to convert raw html files into Mithril's view.js files.

The majority of the code is from Leo Horie (https://github.com/lhorie). 
Original code from Leo was a web page that converted html string (http://lhorie.github.io/mithril/tools/template-converter.html). This script converts the web based version for use in gulp. 
Use example in gulp

```
gulp.task('html2mithril', function() {
    // gulp.src -- get html template
    return gulp.src("./header/text.html")
        // pipe through plugin
        .pipe(mithrilify("object", "postRender"))
        //Rename file as view.js
        .pipe(rename('./header/view.js'))
        // set destination
        .pipe(gulp.dest('./'))
});
```

You can watch for changes in the file or files with gulp watch. 

```
var paths = {
    htmlfile : './header/text.html'
};

gulp.task('watch', function() {
    gulp.watch(paths.htmlfile, ['html2mithril']);

});

gulp.task('default', ['html2mithril', 'watch']);
```

It takes two arguments :
### object (string) 
The module object that the view binds to. for example if your mithril structure is like this:
```
var header = {}
header.controller = function(){}
header.view = function(){} 
```
In this case your object is a string called "header". 

### postRender (string)
If you would like to run a function for rendering when div is loaded you can add it into the wrapper div element. This will appear as :
```
m('div', {config: postRender, [ m(...)])
```
