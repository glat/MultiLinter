# MultiLinter
VisualStudio multiple and customizable linting made easy

#### Short Description
MultiLinter allows you to use in VS2017 several standard linters available by Node.js such as (but not only) ESLint, JSLint, JSHint, Stylelint, CssLint, sass-lint.

#### Why Multilinter?
It was born because the linting integrated in VS2017 is now old. It features old version of linters and no way to change them.

#### How to configure it?
MultiLinter has few options in VS2017. It allows you only to enable a verbose debug to find some configuration error or to enable/disable multiple linting. Yes! You can lint same file with several linters, if you want.

First step is to configure it by editing the default config file which placed in "%USERPROFILE%\.multilinterrc.json" path. This is a Json file which overrides the internal configuration you can find in repository file.

Usually you need to override at least three properties for integrated linters, by this way:

`{ "eslint": { enable: true, additionalArguments: "", fileExtensions: "js" }`

It enables the eslint linter with no additional arguments other than the required one and enables it to be used on .js files.

MultiLinter allows only to interface VS2017 to Node.js linters. It does not install Node.js or linters. **You must set up the environment by properly installing Node.js and your favorite linters in global or local mode in your project. Then, you must create a config file to enable linters them on needed file extensions**.

#### Multiple linting?
So I can use only the integrated linters? The answer is no. If you add new linters in your configuration you can use other ones. See advanced section for this.

If you enables multiple linting in VS2017 options and associates two or more linters for a single file extension MultiLinter will lint that files with every linter and will show you all results in errors windows of VS2017. This is disabled by default.

#### Configuration file
Configuration file is found in same ways Node.js. Searching starts from the current file to be lint directory up to the disk root.
The configuration file must be named ".multilinterrc.json" or ".multilinterrc", same way as several linters.

#### Advanced
You can modify behaviour of MultiLinter, disable integrated linters or add new ones by changing its configuration.

Json config file is a list of linter which overrides the default config (see config.json in repository).

Each linter has these options:
- enabled (boolean): enables or disables these linter.
- additionalArguments (string): additional argument you can use to add other options to the linter (pay attention to quote any arguments, if needed).
- fileExtensions (string): comma separated file extension where to apply this linter (ex: "js,jsx", no dots).
- executable (string): executable to call the linter (ex: eslint.cmd).
- arguments (string): arguments to call the linter. "{filePath}" will be replaced with the file path. You've to include options to get a json formatted result.
- installationType (string): "global" or "local". If global MultiLinter will use the global installed linter, otherwise the local one, searching from file to be lint directory up to the disk root.
- ruleHelpUrl (string): if linter provides web pages to describe warnings/errors this url will allows you to get immediate help for the warning/error clicked. "{ruleId}" will be replaced with the rule id of the warning/error.
- resultsSelector (string): JsonPath selector to extract a JArray from the results got by the linter. This allows MultiLinter to retrieve all results.
- sourceSelector (string): JsonPath selector relative to the JArray results (see resultsSelector) to retrieve the "Source" property of the warning/error.
- lineSelector (string): as previous for line number.
- columnSelector (string): as previous for column number.
- endLineSelector (string): as previous for end line number.
- endColumnSelector (string): as previous for end column number.
- isFatalSelector (string): as previous for isFatal property.
- messageSelector (string): as previous for text warning/error.
- ruleIdSelector (string): as previous for rule id property.
- ruleHelpUrlSelector (string): as previous to extract url to get help for this warning/error.
- severitySelector (string): as previous for severity property. MultiLinter will detect if it's a warning or an error.
