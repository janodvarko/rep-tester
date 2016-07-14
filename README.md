Rep Tester
==========
This tool is intended as simple <b>Reps</b> tester. It connects to the back-end
running in <i>the</i> browser and attaches to the first tab. At this moment,
you need to make sure this page is <i>not</i> the first tab otherwise it
would attach to itself and cause the browser to freeze. This is known limitation
and will be fixed later.

The common scenario is:
1. Launch Firefox and open this tool twice in two tabs.
2. Select the second tab and connect (to the first one).


Source Directory Structure
--------------------------
Since this app loads source modules directly from Firefox source directory,
paths must be properly set.

Here is the default supported directory structure.
(if you use the same directory alignment you don't need to setup anything)


```
<root>
  - mozilla.org
    - fx-team
      + devtools
  - github.com
    - janodvarko
      + rep-tester
```

* `devtools` Root directory for Firefox built-in devtools
* `rep-tester` Root directory for this tool

Webpack config is using the following alias (see `webpack.config` file):

`devtools" => config.firefoxSrc + "/devtools"`

This allows requiring devtools modules (directly from Firefox source dir) as follows:

`require("devtools/client/shared/components/reps/grip");`

Setup
-----

All you need to do is set `firefoxSrc` in `config.js` to point to your
Firefox source directory.

The default is:

```
module.exports = {
  firefoxSrc: "../../../mozilla.org/fx-team"
};
```

Run
---
1. `npm install`
2. `webpack`
3. Load `index.html` in Firefox (using your local web server)
4. Follow instructions on the page

Comments
--------
A few more notes about the config:

* React modules are included in `index.html` and marked as external
in `webpack.config`. This makes the bundling process a bit faster.
* Modules coming from the `devtools` directory are not compiled by Babel.
