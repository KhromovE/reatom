<div align="center">
<br/>

[![reatom logo](https://artalar.github.io/reatom/logos/logo.svg)](https://artalar.github.io/reatom)
</div>

# @reatom/react

Package for bindings [Reatom](https://github.com/artalar/reatom) store with React

[![npm](https://img.shields.io/npm/v/@reatom/react?style=flat-square)](https://www.npmjs.com/package/@reatom/react)
![npm type definitions](https://img.shields.io/npm/types/@reatom/react?style=flat-square)
[![npm bundle size](https://img.shields.io/bundlephobia/minzip/@reatom/react?style=flat-square)](https://bundlephobia.com/result?p=@reatom/react)
![GitHub](https://img.shields.io/github/license/artalar/reatom?style=flat-square)

> Reatom is **declarative** and **reactive** state manager, designed for both simple and complex applications. See [docs](https://artalar.github.io/reatom/).

> **IMPORTANT!** Current state is **Work In Progress**. We do not recommend to use in production at the moment, but... We look forward to your feedback and suggestions to improve the API

> **v1.0.0 schedule**: end of September 2019

## Install

```sh
yarn add @reatom/react
# or
npm i @reatom/react
```

> `@reatom/react` is depend and work with `@reatom/core`

## Hooks Api

### useAtom

Connects the atom to the store represented in context and returns the state of the atom from the store (or default atom state)

#### Basic

```ts
const atomValue = useAtom(atom)
```

#### Depended value by selector

```ts
const atomValue = useAtom(atom, atomState => atomState[props.id], [props.id])
```

#### Mount without subscription (for subscribing atoms to actions)

```ts
const atomValue = useAtom(atom, () => null, [])
```

### useAction

Binds action with dispatch to the store provided in the context

```ts
const handleDoSome = useAction(doSome)
// or
const handleDoSome = useAction(value => myAction({ id: props.id, value }), [props.id])
``` 

## Usage

### Step 1. Create store
```jsx
// App

import React from 'react';
import { createStore } from '@reatom/core'
import { context } from '@reatom/react'
import { Form } from './components/Form'

import './App.css';

export const App = () => {
  // create statefull context for atoms execution
  const store = createStore();

  return (
    <div className='App'>
      <context.Provide value={store}>
        <Form />
      </context.Provide>
    </div>
  );
}
```

### Step 2. Use in component

```jsx
// components/Counter

import { declareAction, declareAtom } from '@reatom/core'
import { useAction, useAtom } from '@reatom/react'

const changeName = declareAction()
const nameAtom = declareAtom('', on => [
  on(changeName, (state, payload) => payload)
])

export const Counter = () => {
  const name = useAtom(nameAtom)
  const handleChangeName = useAction(e => changeName(e.target.value))

  return (
    <form>
      <label forId="name">Enter your name</label>
      <input id="name" value={name} onChange={handleChangeName}/>
    </form>
  )
}
```
