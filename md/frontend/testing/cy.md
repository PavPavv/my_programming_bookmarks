# Cypress

## How to test complex commercial frontend SPA with Cypress?

- [Most common bad cases to avoid](https://docs.cypress.io/app/core-concepts/best-practices)

### Installation

```bash
npm install cypress --save-dev
```

_cypress.config.ts_ config for Angular, for example:

```javascript
import { defineConfig } from "cypress";

export default defineConfig({
  e2e: {
    baseUrl: "http://localhost:4200",
    supportFile: "cypress/support/e2e.ts",
    defaultCommandTimeout: 5000,
    retries: {
      runMode: 3,
      openMode: 3,
    },
  },
  component: {
    devServer: {
      framework: 'angular',
      bundler: 'webpack',
    },
    specPattern: '**/*.cy.ts',
  },
});
```

### Running cypress

Before running the tests, make sure your application local dev-server is running.
Then use _package.json_ command for running cypres in headed ("open") or headless("run") mode.

```json
{
  "scripts": {
    "cy:open": "cypress open",
    "cypress:run": "cypress run --browser chrome"
  }
}
```

```bash
npm run cypress:run
```

### Write tests

In contrast to unit test libraries like "Jest" or whatever, cypress requires write tests in the single "e2e" folder inside "cypress" folder in the root directory.
Like, "./cypress/e2e/first-page-test/header.cy.js" or "./cypress/e2e/first-page-test/header.cy.ts". You can organize tests inside _e2e_ folder whatever you want,
Cypress will find and run them automatically.

- node_modules
- cypress
  - e2e
    - my-first-page
      - my-first-test.cy.js
- src
- package.json

### Queries

Use data attributes as query selector.

```html
<section class="section" data-uitest="main-section-wrap">
  <div>Section</div>
</section>
```

```javascript
cy.get('[data-uitest=main-section-wrap]');
```

### Common API calls

Never use "after" or "afterEach" hooks to clean up the state or run common test for every test.
Most common api calls is is better to organize inside "beforeEach" hook with alias.

```javascript
  beforeEach(() => {
    cy.viewport(1440, 990);
    cy.intercept('http://192.168.100.9:8185/api/**', (req) => {
      req.headers['x_custom_header'] = 'SomeInfo';
    }).as('apiCall);
    cy.visit(requiredExample["loginUrl"]);
  });
```

### Avoid too many unnecessary wait hooks

In a large complex app it is almost impossible to get off of "wait" hook, so just try to implement previous pattern and then use "wait" with it.

```javascript
  it('Some test', () => {
    cy.wait('@apiCall').then(() => {
      // Following tests
    });
  });
```
