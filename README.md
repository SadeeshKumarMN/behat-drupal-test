## Behat Test Execution SetUp for  Drupal8+MAMP Project along with VSCode Extensions Settings

### SetUp for Behat Test Execution:

1. Clone this repo/project which has all the drupal and behat dependencies

2. Move all the child directories of this project(from "core" directory till web.config file) under your MAMP server location (/Applications/MAMP/htdocs)

3. behat.yml file

```
default:
  suites:
    default:
      paths:
        features: '/Applications/MAMP/htdocs/features'
      contexts:
        - FeatureContext
        - Drupal\DrupalExtension\Context\DrupalContext
        - Drupal\DrupalExtension\Context\MinkContext
  extensions:
    Drupal\MinkExtension:
      goutte: ~
      selenium2: ~
      base_url: http://localhost:8888
    Drupal\DrupalExtension:
      blackbox: ~
      api_driver: 'drupal'
      drush:
        alias: 'local'
      drupal:
        drupal_root: '/Applications/MAMP/htdocs/'
```

4. Execute your behat tests from /Applications/MAMP/htdocs
   ```
   vendor/bin/behat
   ```

### VSCode Extensions Setup for Behat

 ![vscode_behat_extensions](demo_evidence/vscode.gif)

1. Install the following extensions and after that reload/restart extensions/vscode based on the extension notifications to make them enable.

   a. [Behat Complete](https://marketplace.visualstudio.com/items?itemName=choppedcode.behat-complete)

   b. [Cucumber (Gherkin) Support enhanced for Behat](https://marketplace.visualstudio.com/items?itemName=marcosvfranco.cucumberautocomplete-behat)

   c. [Behat Checker](https://marketplace.visualstudio.com/items?itemName=beeblebrox3.behat-checker)


2. Append the following lines in your settings.json file which can be accessed in your vscode via
   Go to File -> Preferences -> Settings -> Extensions -> Find and click "Edit in settings.json" (OR)
   Hit CTRL + SHIFT + P and type "Open Settings (JSON)"

```
    "[feature]": {
        "editor.defaultFormatter": "alexkrechik.cucumberautocomplete"
    },
    "cucumberautocomplete.steps": [
        "features/bootstrap/FeatureContext.php"
    ],
    "cucumberautocomplete.syncfeatures": "features/*feature",
    "cucumberautocomplete.strictGherkinCompletion": true,
    "editor.quickSuggestions": {
        "comments": false,
        "strings": true,
        "other": true
    },
    "cucumberautocomplete.gherkinDefinitionPart": "(Scenario:)",
    "cucumberautocomplete.stepRegExSymbol": ".",
    "behat.command": "/Applications/MAMP/htdocs/vendor/bin/behat",
    "behat.configFile": "/Applications/MAMP/htdocs/behat.yml",
    "behat.suite": "",
    "behatChecker.configFile":"behat.yml",
    "behatChecker.trigger":"onChange",
    "behatChecker.debug":false,
    "behatChecker.behatPath": "vendor/bin/behat"
```

3. From the Command Palette (Ctrl+Shift+P), Execute the following commands appropriately

   a. behatChecker.updateCache - the extension communicate with behat and ask for step definitions.If you change your php code, run this command to update de cache, so the extension will know about your new/updated steps.

   b. behatChecker.reload - will reload the extension server internal state.

***Important Notes:***

1. Not all the step definitions are able to identify these extensions and certain configurations would require in order to handle all of them. Please refer the required configurations/settings in their respective extensions pages above

2. This setup needs to modify based on your respective behat project directory since to make the [Behat Complete](https://marketplace.visualstudio.com/items?itemName=choppedcode.behat-complete) successful, it requires absolute path of behat reference to be configured.

3. Regarding BLT Set-up, certain modifications are required in both vscode settings.json and BLT project/behat.yml file and seems this is not the recommended approach as per BLT project. Let me have a second word with our expertise for this.

4. These extensions are not completely replace the features offered from [PhpStorm](https://www.jetbrains.com/help/phpstorm/run-debug-configuration-behat.html) but these are working decent enough to speed up your behat tests writing skills in vscode with "Zero" cost.
