<div align="center">
<br/>

[![reatom logo](https://artalar.github.io/reatom/logos/logo.svg)](https://artalar.github.io/reatom)

</div>

# @reatom/core

Core package of [Reatom](https://github.com/artalar/reatom) state manager. 

[![npm](https://img.shields.io/npm/v/@reatom/core?style=flat-square)](https://www.npmjs.com/package/@reatom/core)
![npm type definitions](https://img.shields.io/npm/types/@reatom/core?style=flat-square)
[![npm bundle size](https://img.shields.io/bundlephobia/minzip/@reatom/core?style=flat-square)](https://bundlephobia.com/result?p=@reatom/core)
![GitHub](https://img.shields.io/github/license/artalar/reatom?style=flat-square)


> Reatom is **declarative** and **reactive** state manager, designed for both simple and complex applications. See [docs](https://artalar.github.io/reatom/).


> **IMPORTANT!** Current state is **Work In Progress**. We do not recommend to use in production at the moment, but... We look forward to your feedback and suggestions to improve the API

> **v1.0.0 schedule**: end of September 2019

## Install

Yarn
```
yarn add @reatom/core
```

NPM
```
npm i -S @reatom/core
```

## Usage

```js
import {
  declareAction,
  declareAtom,
  map,
  combine,
  createStore,
} from '@reatom/core'

/**
 * Step 1.
 * Declare actions
 */
const increment = declareAction()

/**
 * Step 2.
 * Declare atoms (like reducers or models)
 */
const Counter = declareAtom(0, on => [
  on(increment, state => state + 1),
])
const CounterDoubled = map(Counter, value => value * 2)
const CountersShape = combine({ Counter, CounterDoubled })

/**
 * Step 3.
 * Create store entry point
 */
const store = createStore(CountersShape)

/**
 * Step 4.
 * Dispatch action
 */
store.dispatch(increment())

/**
 * Step 5.
 * Get action results
 */
store.getState(Counter) // ➜ 1
store.getState(CounterDoubled) // ➜ 2
store.getState(CountersShape) // ➜ { counter: 1, counterDobled: 2 }
```
