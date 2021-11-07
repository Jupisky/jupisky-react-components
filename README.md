# @jupisky/jupisky-react-components

![Badge](https://raw.githubusercontent.com/storybooks/brand/master/badge/badge-storybook.svg)
![GitHub](https://img.shields.io/github/license/jupisky/jupisky-react-components)

This repository contains a set of React components written in TypeScript.

These components are being used to build the [Jupisky](https://github.com/Jupisky/jupisky-ui) web and desktop app.

## How to install

```bash
   yarn add @jupisky/jupisky-react-components

   npm install @jupisky/jupisky-react-components
```

## Integration

This library makes use of [material-ui - 4.X.X](https://material-ui.com/) and [styled-componentes - 5.X.X]() as `peer dependencies`, this means you must install it in your jupisky. Make sure to provide the same version as the one being used by the current version of this library.


Once everything is installed, you have to instantiate a [ThemeProvider](https://styled-components.com/docs/api#themeprovider) from [styled-components](http://styled-components.com/).

This example uses the theme exported by @jupisky/jupisky-react-components. Here, you can extend this theme to customize it to your needs.

```js
import { ThemeProvider } from 'styled-components';
import { theme } from '@jupisky/jupisky-react-components';

import App from './App';

export default () => (
  <ThemeProvider theme={theme}>
    <App />
  </ThemeProvider>
);
```

### Using the same fonts as jupisky

If you want your Jupisky App to have the same fonts as the one used by Jupisky you need to do the following.

```js
import { createGlobalStyle } from 'styled-components';
import avertaFont from '@jupisky/jupisky-react-components/dist/fonts/averta-normal.woff2';
import avertaBoldFont from '@jupisky/jupisky-react-components/dist/fonts/averta-bold.woff2';

const GlobalStyle = createGlobalStyle`
    @font-face {
        font-family: 'Averta';
        font-display: swap;
        src: local('Averta'), local('Averta Bold'),
        url(${avertaFont}) format('woff2'),
        url(${avertaBoldFont}) format('woff');
    }
`;

export default GlobalStyle;
```

And then include it in the root of your Jupisky App.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import GlobalStyles from './global';

import App from './App';

ReactDOM.render(
  <>
    <GlobalStyles />
    <App>
  </>,
  document.getElementById('root')
);
```

## Using the components

You can import every component exported from `@jupisky/jupisky-react-components` in the same way.

```js
import { Text } from '@jupisky/jupisky-react-components';

const App = () => {
  return <Text size="lg">some text</Text>;
};

export default App;
```

## Local development

To develop on your local machine, install the dependencies (including the peer dependencies):
```
yarn
```

Launch the Storybook:
```
yarn storybook
```

## Testing

Snapshot tests are generated automatically from the Storybook stories using the [StoryShots addon](https://github.com/storybookjs/storybook/tree/master/addons/storyshots/storyshots-core).

To run the tests locally:
```
yarn test
```

Alternatively, run `yarn test --watch` to re-run the tests for each modification you do.
Before you commit your changes, you need to update the snapshots and commit them as well. To do so, run `yarn test -u`.
When the command finishes, the resulting snapshots will be the new baseline.

If you want to add a new Jest test, make sure to put a file with the `.test.tsx` extension into the same directory as the corresponding component.
