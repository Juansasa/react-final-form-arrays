# 🏁 React Final Form Arrays

[![NPM Version](https://img.shields.io/npm/v/react-final-form-arrays.svg?style=flat)](https://www.npmjs.com/package/react-final-form-arrays)
[![NPM Downloads](https://img.shields.io/npm/dm/react-final-form-arrays.svg?style=flat)](https://www.npmjs.com/package/react-final-form-arrays)
[![Build Status](https://img.shields.io/travis/erikras/react-final-form-arrays/v6.svg?style=flat)](https://travis-ci.org/erikras/react-final-form-arrays)
[![codecov.io](https://codecov.io/gh/erikras/react-final-form-arrays/branch/master/graph/badge.svg)](https://codecov.io/gh/erikras/react-final-form-arrays)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)

---

## Installation

```bash
npm install --save react-final-form-arrays react-final-form final-form final-form-arrays
```

or

```bash
yarn add react-final-form-arrays react-final-form final-form final-form-arrays
```

## Usage

🏁 React Final Form Arrays provides a way to render arrays in 🏁 React Final
Form.

```js
import { Form, Field } from 'react-final-form'
import arrayMutators from 'final-form-arrays'
import { FieldArray } from 'react-final-form-arrays'

const MyForm = () => (
  <Form
    onSubmit={onSubmit}
    mutators={{
      // potentially other mutators could be merged here
      ...arrayMutators
    }}
    validate={validate}
    render={({ handleSubmit, pristine, invalid }) => (
      <form onSubmit={handleSubmit}>
        <FieldArray name="customers">
          {({ fields }) => (
            <div>
              {fields.map((name, index) => (
                <div key={name}>
                  <div>
                    <label>First Name</label>
                    <Field name={`${name}.firstName`} component="input" />
                  </div>
                  <div>
                    <label>Last Name</label>
                    <Field name={`${name}.lastName`} component="input" />
                  </div>
                  <button type="button" onClick={() => fields.remove(index)}>
                    Remove
                  </button>
                </div>
              ))}
              <button
                type="button"
                onClick={() => fields.push({ firstName: '', lastName: '' })}
              >
                Add
              </button>
            </div>
          )}
        </FieldArray>
      </form>
    )}
  />
)
```

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->

<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Examples

### [Simple Example](https://codesandbox.io/s/ww40y2m595)

Uses the built-in React inputs: `input`, `select`, and `textarea` to build a
form with no validation.

## Rendering

There are three ways to tell `<FieldArray/>` what to render:

| Method                          | How it is rendered                                        |
| ------------------------------- | --------------------------------------------------------- |
| `component` prop                | `return React.createElement(this.props.component, props)` |
| `render` prop                   | `return this.props.render(props)`                         |
| a render function as `children` | `return this.props.children(props)`                       |

## API

The following can be imported from `react-final-form-arrays`.

### `FieldArray : React.ComponentType<FieldArrayProps>`

A component that takes [`FieldArrayProps`](#fieldarrayprops) and renders an
array of fields

### `version: string`

The current used version of 🏁 React Final Form Arra Array.

---

## Types

### `FieldArrayProps`

These are props that you pass to
[`<FieldArray/>`](#fieldarray--reactcomponenttypefieldarrayprops). You must
provide one of the ways to render: `component`, `render`, or `children`.

#### `children?: ((props: FieldArrayRenderProps) => React.Node) | React.Node`

A render function that is given
[`FieldArrayRenderProps`](#fieldarrayrenderprops), as well as any non-API props
passed into the `<FieldArray/>` component.

#### `component?: React.ComponentType<FieldArrayRenderProps>`

A component that is given [`FieldArrayRenderProps`](#fieldarrayrenderprops) as
props, as well as any non-API props passed into the `<FieldArray/>` component.

#### `name: string`

The name of your field array.

#### `render?: (props: FieldArrayRenderProps) => React.Node`

A render function that is given
[`FieldArrayRenderProps`](#fieldarrayrenderprops), as well as any non-API props
passed into the `<FieldArray/>` component.

#### `subscription?: FieldSubscription`

A
[`FieldSubscription`](https://github.com/erikras/final-form#fieldsubscription--string-boolean-)
that selects of all the items of
[`FieldState`](https://github.com/erikras/final-form#fieldstate) that you wish
to update for. If you don't pass a `subscription` prop, it defaults to _all_ of
[`FieldState`](https://github.com/erikras/final-form#fieldstate).

#### `validate?: (value: ?any[], allValues: Object) => ?any`

A function that takes the field value, and all the values of the form and
returns an error if the array value is invalid, or `undefined` if the value is
valid.

### `FieldArrayRenderProps`

These are the props that
[`<FieldArray/>`](#fieldarray--reactcomponenttypefieldarrayprops) provides to
your render function or component. This object is divided into a `fields` object
that mimics an iterable (e.g. it has `map()` and `forEach()` and `length`), and
`meta` data about the field array. Keep in mind that **the values in `meta` are
dependent on you having subscribed to them** with the
[`subscription` prop](#subscription-fieldsubscription)

#### `input.name: string`

The name of the field.

#### `fields.forEach: (iterator: (name: string, index: number) => void) => void`

Iterates through all of the names of the fields in the field array in bracket
format, e.g. `foo[0]`, `foo[1]`, `foo[2]`.

#### `fields.insert: (index: number, value: any) => void`

A function to insert a value into any arbitrary index of the array.

#### `fields.map: (iterator: (name: string, index: number) => any) => any[]`

Iterates through all of the names of the fields in the field array in bracket
format, e.g. `foo[0]`, `foo[1]`, `foo[2]`, and collects the results of the
iterator function. You will use this in almost every implementation.

#### `fields.move: (from: number, to: number) => void`

A function to move a value from one index to another. Useful for drag-and-drop
reordering.

#### `fields.name: string`

The name of the field array.

#### `fields.pop: () => any`

A function to remove a value from the end of the array. The value will be
returned.

#### `fields.push: (value: any) => void`

A function to add a value to the end of the array.

#### `fields.remove: (index: number) => any`

A function to remove a value from an arbitrary index of the array.

#### `fields.shift: () => any`

A function to remove a value from the beginning of the array. The value will be
returned.

#### `fields.swap: (indexA: number, indexB: number) => void`

A function to swap two values in the array.

#### `fields.unshift: (value: any) => void`

A function to add a value to the beginning of the array.

#### `meta.active?: boolean`

[See the 🏁 Final Form docs on `active`](https://github.com/erikras/final-form#active-boolean).

#### `meta.data: Object`

[See the 🏁 Final Form docs on `data`](https://github.com/erikras/final-form#data-object).

#### `meta.dirty?: boolean`

[See the 🏁 Final Form docs on `dirty`](https://github.com/erikras/final-form#dirty-boolean).

#### `meta.error?: any`

[See the 🏁 Final Form docs on `error`](https://github.com/erikras/final-form#error-any).

#### `meta.initial?: any`

[See the 🏁 Final Form docs on `initial`](https://github.com/erikras/final-form#initial-any).

#### `meta.invalid?: boolean`

[See the 🏁 Final Form docs on `invalid`](https://github.com/erikras/final-form#invalid-boolean).

#### `meta.pristine?: boolean`

[See the 🏁 Final Form docs on `pristine`](https://github.com/erikras/final-form#pristine-boolean).

#### `meta.submitError?: any`

[See the 🏁 Final Form docs on `submitError`](https://github.com/erikras/final-form#submiterror-any).

#### `meta.submitFailed?: boolean`

[See the 🏁 Final Form docs on `submitFailed`](https://github.com/erikras/final-form#submitfailed-boolean).

#### `meta.submitSucceeded?: boolean`

[See the 🏁 Final Form docs on `submitSucceeded`](https://github.com/erikras/final-form#submitsucceeded-boolean).

#### `meta.touched?: boolean`

[See the 🏁 Final Form docs on `touched`](https://github.com/erikras/final-form#touched-boolean).

#### `meta.valid?: boolean`

[See the 🏁 Final Form docs on `valid`](https://github.com/erikras/final-form#valid-boolean).

#### `meta.visited?: boolean`

[See the 🏁 Final Form docs on `visited`](https://github.com/erikras/final-form#visited-boolean).