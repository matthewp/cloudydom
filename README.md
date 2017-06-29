# cloudydom

cloudydom is a shim for ShadowDOM. It is a fork of webcomponents/shadydom, with some bug fixes not present in that project.

## Install

Yarn:

```shell
yarn add cloudydom
```

## Why fork

shadydom is maintained by the Polymer team. They've done fantastic work creating a workable polyfill. However some problems have persisted:

* Although it is regularly committed to, only issues discovered by Polymer are addressed.
* Pull requests made by non-Polymer devs are ignored.
* Issues filed by non-Polymer devs are usually not commented on, even to say "sorry, we do not have time for this right now."
* There hasn't yet been any releases, so using the polyfill through a package manager is difficult.
* Test infrastructure exists but without instructions on how to run the tests it's difficult (impossible?) to add new tests.

**cloudydom** seeks only to address these community issues. Our plan is to:

* Do regular releases as issues are fixed. cloudydom is 1.0 on npm and bower *right now*.
* If you submit a good PR that gets merged, you'll be added a contributor and have push access like anyone else.
* Answer issues in some way. No one is obligated to fix issues, of course, but we'll at least let you know that a PR is welcome!
* Fix the test infrastructure and set up CI so that the project can be maintained with confidence.
* Regularly pull from webcomponents/shadydom#master so that any bug fixes that happen there are fixed in cloudydom as well.

## Usage

Usage of the shim is transparent when `attachShadow` is unavailable. Elements are
patched as needed to report ShadowDOM correct DOM information. Only DOM tree
accessors and mutation api is maintained. Some DOM api
(for example MutationObservers) is not shimmed.

To force cloudydom to be used even when native ShadowDOM is available, set
the `ShadyDOM = {force: true}` in a script prior to loading the polyfill.

## Example

```html
<div id="host"></div>
<script>
  host.attachShadow({mode: 'open'});
  host.shadowRoot.appendChild(document.createElement('a'));
</script>

```

## Building and Testing

For building and testing, first run
```
npm install
bower install
```

To build, make sure gulp is installed and `gulp`.

To test, run `npm test`


## Limitations

cloudydom distribution is asynchronous for performance reasons. This means that
the composed DOM will be available 1 microtask after the DOM mutation occurs.
For testing, `ShadyDOM.flush` may be called to force synchronous composition.

ShadowDOM compatible styling is *not* provided with the ShadyDOM shim. To
shim ShadowDOM styling, use the [shadycss](https://github.com/webcomponents/shadycss) shim.
