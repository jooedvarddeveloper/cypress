# Install Typescript
```bash
npm install typescript --save-dev
```

# create a tsconfig.json file
```json
{
  "compilerOptions": {
    "target": "es6",
    "lib": ["es6", "dom"],
    "sourceMap": true,
    "types": ["cypress", "node"],
    "moduleResolution": "node16",
    "module": "node16"
  },
  "include": ["**/*.ts"]
}
```

# Install Cypress
```bash
npm install cypress --save-dev
```

# Make your own start command in package.json
```json
"scripts": {
    "start:cypress": "npx cypress open"
}
```

# Install Cucumber
```bash
npm i @badeball/cypress-cucumber-preprocessor
npm i @bahmutov/cypress-esbuild-preprocessor
```

# Create a cypress.config.ts
```typescript
import { defineConfig } from "cypress";
import createBundler from "@bahmutov/cypress-esbuild-preprocessor";
import { addCucumberPreprocessorPlugin } from "@badeball/cypress-cucumber-preprocessor";
import createEsbuildPlugin from "@badeball/cypress-cucumber-preprocessor/esbuild";

export default defineConfig({
  e2e: {
    specPattern: "**/*.feature",
    supportFile: false,
    async setupNodeEvents(
      on: Cypress.PluginEvents,
      config: Cypress.PluginConfigOptions
    ): Promise<Cypress.PluginConfigOptions> {
      await addCucumberPreprocessorPlugin(on, config);
      on(
        "file:preprocessor",
        createBundler({
          plugins: [createEsbuildPlugin(config)],
        })
      );
      return config;
    },
  },
});
```

# LOCALIZATION

| Feature | Jellemző |
|---------|----------|
| Background | Háttér |
| Rule | Szabály |
| Scenario | PéldaForgatókönyv |
| Scenario Outline | Forgatókönyv vázlat |
| Examples | Példák |
| Given | *AmennyibenAdott |
| When | *MajdHaAmikor |
| Then | *Akkor |
| And | *És |
| But | *De |
```gherkin
language: hu
Jellemző: Localhost Betölt
Forgatókönyv: Első teszt esetem
  Amikor meglátogatom a localhost-ot
  Akkor az oldal title tag-je tartalmazza Hello
```
