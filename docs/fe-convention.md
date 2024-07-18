# Coding convention for JS & FrameworkJS


## Table of Contents
1. [JS coding conventions](#js-coding-conventions)
    1. [80 characters per line](#80-characters-per-line)
    2. [Use single quotes](#use-single-quotes)
    3. [Opening braces go on the same line](#opening-braces-go-on-the-same-line)
    4. [Use lowerCamelCase for variables, properties and function names](#use-lowercamelcase-for-variables-properties-and-function-names)
    5. [Use UpperCamelCase for class names, components](#use-uppercamelcase-for-class-names-components)
    6. [Use UPPERCASE for Constants](#use-uppercase-for-constants)
    7. [Use the === operator](#use-the--operator)
    8. [Use descriptive conditions](#use-descriptive-conditions)
    9. [Write small functions](#write-small-functions)
    9. [Return early from functions](#return-early-from-functions)
    10. [No nested closures](#no-nested-closures)
2. [TS coding conventions](#ts-coding-conventions)
    1. [Do not use null](#do-not-use-null)
    2. [Do not use any](#do-not-use-any)
    3. [Filename](#filename)
3. [Vue coding conversions](#vue-coding-conversions)
    1. [Order in a composition/vue](#order-in-a-compositionvue)
    2. [Component filename](#component-filename)
    3. [Composition filename](#composition-filename)
    4. [Tightly coupled component names](#tightly-coupled-component-names)
    4. [Full-word component names](#full-word-component-names)
    5. [Use child component in parent](#use-child-component-in-parent)
    6. [Ref vs Reactive](#ref-vs-reactive)
    7. [Props](#props)
    8. [Prop name casing](#prop-name-casing)
    9. [Emit events](#emit-events)
    10. [Directive shorthands](#directive-shorthands)
    11. [Provide / Inject should not be used](#provide--inject-should-not-be-used)
    12. [Async Components in Vue 3](#async-components-in-vue-3)
    12. [Components & composition](#components--composition)
## JS coding conventions

#### 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

#### Use single quotes

Use single quotes, unless you are writing JSON.

✅ Do

```ts
let foo = 'bar';
```

❌ Don't

```ts
let foo = "bar";
```

#### Opening braces go on the same line

Your opening braces go on the same line as the statement.

✅ Do
 
```ts
if (true) {
  console.log('winning');
}
```

❌ Don't

```ts
if (true) {
  console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement.

#### Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`. They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

✅ Do

```ts
let adminUser = '';
function barFunc() { }
```

❌ Don't

```ts
let admin_user = '';
function bar_func() { }
function BarFunc() { }
```

#### Use UpperCamelCase for class names, components

Class names should be capitalized using `UpperCamelCase`.

✅ Do

```ts
const BankAccount = ()=> {};
class BankAccount = {}
```

❌ Don't

```ts
const bankAccount = ()=> {};
class Bank_Account = {}
```

#### Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties, using all uppercase letters. Use `const` to create variable


✅ Do

```ts
const SECOND = 1 * 1000;

let File = {}
File.FULL_PERMISSIONS = 0777;
```

❌ Don't

```ts
const second = 1 * 1000;

let File = {}
File.fullPermissions = 0777;
```

#### Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

✅ Do

```ts
if (a !== '') {}
```

❌ Don't

```ts
if (a != '') {}
```

#### Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

✅ Do

```ts
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log("winning");
}
```

❌ Don't

```ts
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log("losing");
}
```

#### Write small functions

Keep your functions short. A good function fits on a slide that the people in the last row of a big room can comfortably read. So don't count on them having perfect vision and limit yourself to ~15 lines of code per function.

#### Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

✅ Do

```ts
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

❌ Don't

```ts
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```ts
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

#### No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

✅ Do

```ts
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

❌ Don't

```ts
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```

## TS coding conventions

#### Do not use null

Use `undefined`. Do not use `null` except where external libraries require it.

✅ Do

```ts
let userType = undefined
```

❌ Don't

```ts
let userType = null
```

#### Do not use any

Do not use `any` anywhere in the code.

✅ Do

```ts
type Result = "success" | "failure"
function verifyResult(result: Result) {
    if (result === "success") {
        console.log("Passed");
    } else {
        console.log("Failed")
    }
}
```

❌ Don't

```ts
function verifyResult(result: any) {
    if (result === "success") {
        console.log("Passed");
    } else {
        console.log("Failed")
    }
}
```

#### Filename

Name files with `camelCase`. E.g. `utils.ts`, `map.ts` etc.

✅ Do

```ts
getUser.ts
```

❌ Don't

```ts
getuser.ts
get-user.ts
get_user.ts
GetUser.ts
Get_User.ts
```

## Vue coding conversions

#### Order in a composition/vue

```ts
<script lang="ts" setup>
// Import vue & library
import { defineComponent, PropType } from 'vue';

// Components
import TodoItem from './components/todo.vue';

// Composition
import useTodo from './composition/useTodo';

// Define prop types
type Props = {
  items: string[];
};

// Prop variable
const props = defineProps<Props>();
const props = withDefaults(defineProps<Props>(), {
  items: ['Item 1', 'Item 2'],
});

// Emit events
const emit = defineEmits<{
  (e: 'deleteTodo', todoId?: string): void;
}>();

// Composition
const { deleteTodo } = useTodo();

// Ref
const todoName = ref<string | null>('');

// Computed
const itemLen = computed(() => props.items.length);

// Function handle
const handleDelete = () => {};

// Function listen event
const onDelete = () => {};

// Watch & event watch
watch(itemLen, () => {});

// onMounted
onMounted(() => {});

// onUnmounted
onUnmounted(() => {});
</script>
```

#### Component filename

The name of a file component should be in `PascalCase`

✅ Do

```ts
components/
|- MyComponent.vue
```

❌ Don't

```ts
components/
|- mycomponent.vue
components/
|- myComponent.vue
components/
|- my-component.vue
```

#### Composition filename

The name of a file composition should be in `camelCase`. Start with the `use` keyword

✅ Do

```ts
composition/
|- useMyComposition.ts
```

❌ Don't

```ts
composition/
|- usemycomposition.ts
composition/
|- myComposition.ts
composition/
|- use-my-composition.vue
```

#### Tightly coupled component names

✅ Do

```ts
components/
|- TodoList.vue
|- TodoListItem.vue
```

❌ Don't

```ts
components/
|- TodoList.vue
|- TodoItem.vue
```

#### Full-word component names

✅ Do

```ts
components/
|- StudentDashboardSettings.vue
|- UserProfileOptions.vue
```

❌ Don't

```ts
components/
|- SdSettings.vue
|- UProfOpts.vue
```

#### Use child component in parent

Use a component with `PascalCase` syntax

✅ Do

```ts
<MyComponent/>
```

❌ Don't

```ts
<myComponent/>

<my-component/>
```

#### Ref vs Reactive

There is a lot of discussions out there about when to use what. I find that when working with primitives, always go with `ref()`. When working with objects, go with `reactive()`

```ts
const myName = ref<string>('Nicky')

type User = {
  name: string
  age: number
}
const user: User = reactive({
  name: 'Nicky',
  age: 37
});
```

*Types are **required** when using `ref` and `reactive`*

#### Props

✅ Do

```ts
type Props = {
  items: string[];
};
const props = defineProps<Props>();

or 

const props = defineProps<{
  items: string[];
}>();
```

❌ Don't

```ts
defineProps({
  items: string[]
})

const props = defineProps(['items'])
```

*Use variable `const props =`, do not use `const prop =`*


#### Prop name casing

Prop names should always be declared as `camelCase` but use `kebab-key` in templates

✅ Do

```ts
props: {
  greetingText: String
}
<WelcomeMessage greeting-text="hi"/>
```

❌ Don't

```ts
props: {
  'greeting-text': String
}
<WelcomeMessage greetingText="hi"/>
```

#### Emit events

Need to define props separately instead of nesting in defineProps function

✅ Do

```ts
const emit = defineEmits<{
  (e: 'change', id: number): void
  (e: 'update', value: string): void
}>()
```

❌ Don't

```ts
defineEmits(['inFocus', 'submit'])

const emit = defineEmits(['inFocus', 'submit'])
```

*Use variable `const emit =`, do not use `const emits =`*

#### Directive shorthands

Use directive with `:`, `@` instead of `v-bind`, `v-on`

✅ Do

```ts
<input
  :class="{ active: isActive }"
  @focus="onFocus"
>
```

❌ Don't

```ts
<input
  v-bind:class="{ active: isActive }"
  v-on:focus="onFocus"
>
```

#### Provide / Inject should not be used

Passing data from parent to deep child should use store (Pinia).

Pinia: https://pinia.vuejs.org/

#### Async Components in Vue 3

You should try making use of Async Components. This can dramatically speed up your application as you don’t pollute your main bundle with code you don't necessarily need. The cool thing about async functions is you only load the code when the client needs it and thereby keeping your JS bundle to a minimum

```ts
//From the vue docs > https://v3.vuejs.org/guide/migration/async-components.html#introduction
import { defineAsyncComponent } from 'vue'
import ErrorComponent from './components/ErrorComponent.vue'
import LoadingComponent from './components/LoadingComponent.vue'

// Async component without options
const asyncModal = defineAsyncComponent(() => import('./Modal.vue'))

// Async component with options
const asyncModalWithOptions = defineAsyncComponent({
  loader: () => import('./Modal.vue'),
  delay: 200,
  timeout: 3000,
  errorComponent: ErrorComponent,
  loadingComponent: LoadingComponent
})
```

#### Components & Composable

All functions, variables, watches should be separated into composable. `Do not write to .vue`

```ts
// event.js
import { onMounted, onUnmounted } from 'vue'

export function useEventListener(target, event, callback) {
  onMounted(() => target.addEventListener(event, callback))
  onUnmounted(() => target.removeEventListener(event, callback))
}
```

```ts
// mouse.js
import { ref, onMounted, onUnmounted } from 'vue'

export function useMouse() {
  const x = ref(0)
  const y = ref(0)

  useEventListener(window, 'mousemove', (event) => {
    x.value = event.pageX
    y.value = event.pageY
  })

  return { x, y }
}
```

```ts
<script setup lang='ts'>
import { useMouse } from './mouse.js'

const { x, y } = useMouse()
</script>

<template>Mouse position is at: {{ x }}, {{ y }}</template>
```
