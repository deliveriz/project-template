# JavaScript Project with ESLint, Prettier, Jest, and GitHub Actions

This project demonstrates how to set up a JavaScript application with ESLint and Prettier for code formatting and linting, Jest for testing, and a GitHub Actions workflow.

## Getting Started

To recreate this project, follow these steps:

### 1. Set Up the Project

Ensure you have Node.js installed. Then, initialise a new project:

```bash
npm init -y
```

### 2. Install Dependencies

Install the required packages for linting, formatting, and testing:

```bash
npm install --save-dev eslint prettier eslint-plugin-prettier eslint-config-prettier jest
```

### 3. Create ESLint Configuration

Set up ESLint with a configuration file named `eslint.config.mjs`. Add the following:

```javascript
import prettier from 'eslint-config-prettier';
import prettierPlugin from 'eslint-plugin-prettier';

export default [
  {
    ignores: ['node_modules'],
  },
  {
    files: ['**/*.js'],
    languageOptions: {
      ecmaVersion: 'latest',
    },
    plugins: {
      prettier: prettierPlugin,
    },
    rules: {
      ...prettier.rules,
      'prettier/prettier': 'error',
    },
  },
];
```

### 4. Add Prettier Configuration

Create a `.prettierrc` file to define formatting rules:

```json
{
  "singleQuote": true,
  "semi": true
}
```

### 5. Add Scripts to package.json

Include the following scripts in your `package.json`:

```json
"scripts": {
  "format": "prettier --write .",
  "lint": "eslint .",
  "test": "jest"
}
```

### 6. Create Application Code

Add a file named `math.js` with this content:

```javascript
function addNumbers(a, b) {
  return a + b;
}

module.exports = { addNumbers };
```

### 7. Write a Test File

Create a file named `math.test.js` to test the function:

```javascript
const { addNumbers } = require('./math');

describe('math.js', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(addNumbers(1, 2)).toBe(3);
  });
});
```

### 8. Add a GitHub Actions Workflow

In the `.github/workflows directory`, create a file named `main.yml` with this content:

```yaml
name: JavaScript Workflow

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install dependencies
        run: npm install
      - name: Run Prettier
        run: npm run format
      - name: Run ESLint
        run: npm run lint
      - name: Run tests
        run: npm test
```

### 9. Run Locally

Format code: `npm run format`

Lint code: `npm run lint`

Test code: `npm test`

### 10. Push to GitHub

Commit your changes and push to your GitHub repository. The GitHub Actions workflow will run automatically.
