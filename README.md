# MultiLinter
VisualStudio multiple and customizable linting made easy

#### Short Description
MultiLinter allows you to use in VS2019 several standard linters available by Node.js such as (but not only) ESLint, JSLint, JSHint, Stylelint, CssLint, sass-lint.

#### Why Multilinter?
It was born because the linting integrated in VS2019 is now old. It features old version of linters and no way to change them.

#### How to configure it?
MultiLinter has few options in VS2019. It allows you only to enable a verbose debug to find some configuration error or to enable/disable multiple linting. Yes! You can lint same file with several linters, if you want.

First step is to configure it by editing the default config file which placed (usually) in "%USERPROFILE%\\.multilinterrc.json" path. This is a Json file which overrides the internal configuration you can find in repository file.

Usually you need to override at least three properties for integrated linters, by this way:

`{ "eslint": { enable: true, additionalArguments: "", fileExtensions: "js" }`

It enables the eslint linter with no additional arguments other than the required ones and enables it to be used on .js files.

MultiLinter allows only to interface VS2019 to Node.js linters. It does not install Node.js or linters.

**You must set up the environment by properly installing Node.js and your favorite linters in global or local mode in your project. Then, you must create a config file to enable linters them on needed file extensions**.

**You should also disable internal VS2019 linting**.

#### Can I use only the integrated linters?
The answer is no. If you add new linters in your Json configuration file you can use other ones. See advanced section for this.

#### Multiple linting?
If you enables multiple linting in VS2019 options and associates two or more linters to a single file extension MultiLinter will lint that files with every linter and will show you all results in errors windows of VS2019. This is disabled by default.

#### Configuration file
Configuration file is found in same ways Node.js linters do. Search starts from the current file to be lint directory up to the disk root.

The configuration file must be named ".multilinterrc.json" or ".multilinterrc", same way as several linters.

Usually it is placed in user profile directory.

#### Global or local usage
You can use npm global installed linters or local installed linters. If you enable "Real Time" linting MultiLinter will creates a shadow file named [fileName].multilinter.[fileExtension] in same directory of the original file. It will delete as soon as linting is done. This file can appear for a moment in Visual Studio Explorer. To avoid these files to be shown in Visual Studio Explorer add these lines to your project file (.csproj):

<ItemGroup>
  <None Remove="**\*.multilinter.*" Visible="false" />
  <Content Remove="**\*.multilinter.*" Visible="false" />
  <Compile Remove="**\*.multilinter.*" Visible="false" />
  <EmbeddedResource Remove="**\*.multilinter.*" Visible="false" />
</ItemGroup>

#### Advanced
You can modify behaviour of MultiLinter, enable or disable integrated linters or add new ones by changing its configuration.

Json config file is a list of linters which overrides the default config (see config.json in repository).

Each linter has these options:
- enabled (boolean): enables or disables these linter.
- additionalArguments (string): additional argument you can use to add other options to the linter (pay attention to quote any arguments
