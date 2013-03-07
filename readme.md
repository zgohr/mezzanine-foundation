Include this app in your ```INSTALLED_APPS``` after your style/theme app.

In your style/theme app, create a ```style.scss``` file that imports ```mezz-foundation.scss``` something like this:

```
@import "../../mezzanine-foundation/mezz-foundation.scss"
```

At this point, I recommend using the SASS gem and GruntJS to watch your ```style.scss``` for changes and compile to CSS, but this part is up to you. Another option would be django-compressor.

When overriding Mezzanine templates, make sure to check mezzanine-foundation for its overrides before going to Mezzanine itself.

![screen shot](https://github.com/zgohr/mezzanine-foundation/raw/master/docs/ss.png)

Example package.json and Gruntfile to get you started

```
'use strict';

module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dev: {
        options: {
          style: 'expanded'
        },
        files: {
          'static/theme/style.css': 'scss/style.scss'
        }
      }
    },
    watch: {
      scripts: {
        files: ['scss/style.scss', '../mezzanine-foundation/mezz-foundation.scss'],
        tasks: 'sass'
      }
    }
  });

  grunt.loadNpmTasks('grunt-contrib-watch'); // register contrib tasks
  grunt.loadNpmTasks('grunt-contrib-sass');

  grunt.registerTask('default', ['sass']);
};
```

```
{
  "name": "theme-compiler",
  "version": "0.0.1",
  "engines": {
    "node": ">= 0.8.0"
  },
  "scripts": {
    "preinstall": "npm -g grunt-cli node-static",
    "serve": "grunt; node scripts/serve.js",
    "watch": "grunt watch",
    "grunt": "grunt"
  },
  "dependencies": {
    "grunt-lib-contrib": "~0.3.0"
  },
  "devDependencies": {
    "grunt": "~0.4.0",
    "grunt-contrib-sass": "~0.2.2",
    "grunt-contrib-watch": "~0.3.1"
  }
}
```

