# Off-Canvas Glossary

This glossary supplements the [U.S. Fish and Wildlife Service Southeast Regional website](http://fws.gov/southeast).  The goal of this glossary is to provide definitions to terms that may be unclear to our users. We are focused on writing content in plain language, but terms associated with Rules and Regulations may be foreign to our users.  This glossary automatically searches the current page for glossary terms, highlights them, and makes them clickable.  Clicking a term will summon the glossary from off-screen.  You can find related terms and when you're done reading the definition you can return to your place on the page.

## Usage

```javascript
(function () {
  'use strict';

  var glossary = require('./glossary');
  var highlighter = require('./highlighter');
  var data = require('./get-terms');
  var emitter = require('./mediator');

  data.load({
    url: '../data/terms.json'
  });

  emitter.on('terms:loaded', function (terms) {
    glossary.init({
      appendStyle: 'appendTo',
      target: '.glossary-list'
    });

    highlighter.highlight({
      data: terms,
      content: '',
      element: 'span',
      class: 'highlighted-term'
    });
  })
})();
```

## Options

### Data Access

This module that acts as a data service layer.  It downloads glossary terms via AJAX so the terms can be cached and makes them available to other modules.

- url (string): a valid url for the location of a JSON file containing glossary terms e.x: `'../data/terms.json'`

### Glossary

An html glossary built from an array of JSON documents. The glossary provides full text search using [lunr.js](http://lunrjs.com/).

- active (boolean): Whether or not the glossary is active upon initialization  default: false
- container (selector/DOM node): The containing element default: '.glossary-container'
- terms (array): An array of JSON documents representing glossary terms that will be the basis of our search functionality

### Highlighter

  This module searches a given DOM node and it's children for glossary terms.  The module wraps terms in an element with a class so they can be styled and used to toggle the glossary

 - content (string/dom node): The content area that you'd like to search for glossary terms. default: 'main-content'
 - data (array): An array of JSON documents representing glossary terms that will be the basis with which to search the content area
 - element (string): The type of element you would like to wrap the found term with
 - termClass (string): The class used to highlight any glossary terms found on the page. default: 'glossary-term',

### Development

To ease development we use npm scripts to compile JS with browserify/watchify, compile sass to css, optimize images, etc:

First, install the project dependencies:

`npm install`

To kick off the development server and all pre-requisite tasks:

`npm start`

To build a production ready version of the app use:

`npm run build`

To publish a production ready demo to GitHub Pages:

`npm run publish:demo`

To visualize packages contributing to bundle file size:

`npm run inspect:bundle`

License

This project is a [U.S. Government work](https://www.usa.gov/government-works).

The United States Fish and Wildlife Service (FWS) GitHub project code is provided on an "as is" basis and the user assumes responsibility for its use. FWS has relinquished control of the information and no longer has responsibility to protect the integrity, confidentiality, or availability of the information. Any reference to specific commercial products, processes, or services by service mark, trademark, manufacturer, or otherwise, does not constitute or imply their endorsement, recommendation or favoring by FWS. The FWS seal and logo shall not be used in any manner to imply endorsement of any commercial product or activity by FWS or the United States Government.
