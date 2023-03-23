# CRA with TypeScript
#setup 

## App creation.
We can use a template with CRA:

```shell
npx create-react-app my-app --template typescript
```

## tsconfig

Modify `tsconfig.json`, we want to change `allowJs` from `true` to `false`. This is so we can't compile any JS file, if we're in the process of migrating an existing only JS app to TS, we should set it to `true`.

```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": false,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": [
    "src"
  ]
}
```

The `lib` key in `compilerOptions` tells the Compiler to include the type definitions for things found in the browser.

## ESlint config

Create a `.eslintrc` file with the following content:

```json
{
  "env": {
    "browser": true,
    "es6": true,
    "jest": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "plugins": ["react", "@typescript-eslint"],
  "settings": {
    "react": {
      "pragma": "React",
      "version": "detect"
    }
  },
  "rules": {
    "@typescript-eslint/explicit-function-return-type": 0,
    "@typescript-eslint/explicit-module-boundary-types": 0,
    "react/react-in-jsx-scope": 0
  }
}
```

Since the return type of most React components is generally either _JSX.Element_ or _null_, we have loosened up the default linting rules a bit by disabling the rules [explicit-function-return-type](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/explicit-function-return-type.md) and [explicit-module-boundary-types](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/explicit-module-boundary-types.md). Now we don't need to explicitly state our function return types everywhere. We will also disable [react/react-in-jsx-scope](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/react-in-jsx-scope.md) since importing React is [no longer needed](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html) in every file.

## package.json

We must add a `lint` script so we can parse the `tsx` files:
```json
{
  // ...
    "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "lint": "eslint './src/**/*.{ts,tsx}'"  
    },
  // ...
}
```

# Type Narrowing

If we have data with shared properties and subset of the items share some other properties we can create a Base interface and then extend it to fit our other use cases:

```ts
interface CoursePartBase {
  name: string;
  exerciseCount: number;
}

interface CoursePartBasic extends CoursePartBase {
  description: string;
  kind: "basic"
}

interface CoursePartGroup extends CoursePartBase {
  groupProjectCount: number;
  kind: "group"
}

interface CoursePartBackround extends CoursePartBase {
  description: string;
  backroundMaterial: string;
  kind: "background"
}

type CoursePart = CoursePartBasic | CoursePartGroup | CoursePartBackround;
```

In the code above we have a base `CoursePartBase` and three other "sub" interfaces. We then create a [[Basic Concepts#Discriminated Unions|discriminated union]] using all the specific interfaces. When we try to access the properties of an item in array like `CoursePart[]` we can only access the common properties, in this case `name` && `exerciseCount`, in order to access the specific properties of the other interfaces we must first *narrow* the union with code.

One way to narrow the Union is to use a switch case:

```ts
switch(part.kind){
	case 'basic':
		// we now have acess to the description property
	...
	default:
		break;
}
```

The above code works fine, but what happens if we add a new Course Part to our union? The Part would be handled by the `default` block and nothing would happen. We can then use [[Basic Concepts#Exhaustiveness checking]] to ensure we're handling every type.

The course provides an alternative approach to handling the exhaustiveness check:

```ts
const assertNever = (value: never): never => {
  throw new Error(
    `Unhandled discriminated union member: ${JSON.stringify(value)}`
  );
};
```

We can then use that util function in our Switch statement:

```ts
	...
	default:
		return assertNever(part);
	...
```