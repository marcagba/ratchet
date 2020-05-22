# PropTypes to TS

> Codemod to convert React PropTypes to TypeScript types.

## Key Features

- Supports function and class components
- Supports `static propTypes` declarations on class components
- Supports files with multiple components
- Option to remove or preserve PropTypes after converting to TS

## Usage

Run the following command with a file glob that matches the files you want to convert.

```sh
npx jscodeshift -t https://raw.githubusercontent.com/mskelton/prop-types-to-ts/master/transform.js GLOB

# Example
npx jscodeshift -t https://raw.githubusercontent.com/mskelton/prop-types-to-ts/master/transform.js src/**/*.{js,jsx}
```

## Example Input/Output

```ts
// Input
import PropTypes from "prop-types"
import React from "react"

export function MyComponent(props) {
  return <span />
}

MyComponent.propTypes = {
  bar: PropTypes.string.isRequired,
  foo: PropTypes.number,
}

// Input
import React from "react"

type Props = {
  bar: string
  foo?: number
}

export function MyComponent(props: Props) {
  return <span />
}
```

## Options

### `--preserve-prop-types`

This option will preserve PropTypes after converting to TS. This is useful for component libraries where you support both TypeScript declarations and PropTypes.

#### Input

```js
import PropTypes from "prop-types"
import React from "react"

export function MyComponent(props) {
  return <span />
}

MyComponent.propTypes = {
  bar: PropTypes.string.isRequired,
  foo: PropTypes.number,
}
```

#### Output

```ts
import PropTypes from "prop-types"
import React from "react"

type Props = {
  bar: string
  foo?: number
}

export function MyComponent(props: Props) {
  return <span />
}

MyComponent.propTypes = {
  bar: PropTypes.string.isRequired,
  foo: PropTypes.number,
}
```
