---
id: intl-relativetimeformat
title: Intl.RelativeTimeFormat
---

A spec-compliant polyfill for Intl.RelativeTimeFormat fully tested by the [official ECMAScript Conformance test suite](https://github.com/tc39/test262)

[![npm Version](https://img.shields.io/npm/v/@formatjs/intl-relativetimeformat.svg?style=flat-square)](https://www.npmjs.org/package/@formatjs/intl-relativetimeformat)
![size](https://badgen.net/bundlephobia/minzip/@formatjs/intl-relativetimeformat)

## Installation

import Tabs from '@theme/Tabs'
import TabItem from '@theme/TabItem'

<Tabs
groupId="npm"
defaultValue="npm"
values={[
{label: 'npm', value: 'npm'},
{label: 'yarn', value: 'yarn'},
]}>
<TabItem value="npm">

```sh
npm i @formatjs/intl-relativetimeformat
```

</TabItem>
<TabItem value="yarn">

```sh
yarn add @formatjs/intl-relativetimeformat
```

</TabItem>
</Tabs>

## Requirements

This package requires the following capabilities:

- [`Intl.getCanonicalLocales`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/getCanonicalLocales) or [polyfill](intl-getcanonicallocales.md)
- [`Intl.Locale`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Locale) or [polyfill](intl-locale.md).
- [`Intl.PluralRules`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/PluralRules) or [polyfill](intl-pluralrules.md).
- If you need `formatToParts` and have to support IE11- or Node 10-, you'd need to polyfill using [`@formatjs/intl-numberformat`](intl-numberformat.md).

## Usage

### Simple

```tsx
import '@formatjs/intl-relativetimeformat/polyfill'
import '@formatjs/intl-relativetimeformat/locale-data/en' // locale-data for en
```

### Dynamic import + capability detection

```tsx
import {shouldPolyfill} from '@formatjs/intl-relativetimeformat/should-polyfill'
async function polyfill(locale: string) {
  if (shouldPolyfill()) {
    // Load the polyfill 1st BEFORE loading data
    await import('@formatjs/intl-relativetimeformat/polyfill')
  }

  if (Intl.RelativeTimeFormat.polyfilled) {
    switch (locale) {
      default:
        await import('@formatjs/intl-relativetimeformat/locale-data/en')
        break
      case 'fr':
        await import('@formatjs/intl-relativetimeformat/locale-data/fr')
        break
    }
  }
}
```

## Tests

This library is fully [test262](https://github.com/tc39/test262/tree/master/test/intl402/RelativeTimeFormat)-compliant.
