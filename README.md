# react-i18nify
Simple i18n translation and localization components and helpers for React applications.

[![npm version](https://badge.fury.io/js/react-i18nify.svg)](https://badge.fury.io/js/react-i18nify)

## Preparation

First install the package:
```
npm i react-i18nify --save
```

Next, load the translations to be used, for example in `app.js`:
```javascript
var I18n = require('react-i18nify').I18n;

I18n.loadTranslations({
  en: {
    application: {
      title: 'Awesome app with i18n!',
      hello: 'Hello, %{name}!'
    },
    date: {
      long: 'MMMM Do, YYYY'
    }
  },
  nl: {
    application: {
      title: 'Toffe app met i18n!',
      hello: 'Hallo, %{name}!'
    },
    date: {
      long: 'D MMMM YYYY'
    }
  }
});
```

Finally, you should set the locale to be used:
```javascript
var I18n = require('react-i18nify').I18n;

I18n.setLocale('nl');
```

Now you're all set up to start unleashing the power of `react-i18nify`!

## Components

The easiest way to translate or localize in your React components is by using the `Translate` and `Localize` components:
```javascript
var React = require('react');
var Translate = require('react-i18nify').Translate;
var Localize = require('react-i18nify').Localize;

var AwesomeComponent = React.createClass({
  render: function() {
    return (
      <div>
        <Translate value="application.title"/>
          // => returns '<span>Toffe app met i18n!</span>' for locale 'nl'
        <Translate value="application.hello" name="Aad"/>
          // => returns '<span>Hallo, Aad!</span>' for locale 'nl'
        <Localize value="2015-09-03" dateFormat="date.long"/>
          // => returns '<span>3 september 2015</span> for locale 'nl'
        <Localize value={10/3} options={{style: 'currency', currency: 'EUR', minimumFractionDigits: 2, maximumFractionDigits: 2}}/>
          // => returns '<span>€ 3,33</span> for locale 'nl'
      </div>
    );
  }
});
```

## Helpers

If for some reason, you cannot use the components, you can use the `I18n.t` and `I18n.l` helpers instead:
```javascript
var I18n = require('react-i18nify').I18n;

I18n.t('application.title'); // => returns 'Toffe app met i18n!' for locale 'nl'
I18n.t('application.name', {name: 'Aad'}); // => returns 'Hallo, Aad!' for locale 'nl'

I18n.l(1385856000000, { dateFormat: 'date.long' }); // => returns '1 december 2013' for locale 'nl'
I18n.l(Math.PI, { maximumFractionDigits: 2 }); // => returns '3,14' for locale 'nl'
```

## Supported localize options

The localize component and helper support all date formatting options as provided by the Javascript `moment` library. For the full list of options, see http://momentjs.com/docs/#/displaying/format/.

For number formatting, the localize component and helper support all options as provided by the Javascript built-in `Intl.NumberFormat` object. For the full list of options, see https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat.