# MultiLinter
VisualStudio multiple and customizable linting made easy

#### Short Description
MultiLinter allows you to use in VS2019 several standard linters available by Node.js such as (but not only) ESLint, JSLint, JSHint, Stylelint, CssLint, sass-lint.

#### Why Multilinter?
It was born because the linting integrated in VS2019 is now old. It features old version of linters and no way to change them.

#### Some clarifications

Some GitHub users tryied to stop MultiLinter development placing bad reviews on the VS MarketPlace and bothering me on this repo with questions I do not want to answer to, so, to be clear here are some clarifications about that questions:

1. MultiLinter is **closed source**.
2. MultiLinter is not related in any way with VisualLinter except because VisualLinter author refused a PR I sent to him and this moved me to write ground up a new linter extension.
3. MultiLinter is **not** a fork of VisualLinter.

#### Some warnings

To be clear here are some rules to create an issue on this repo:

1. You can create issues to send bug reports, improvement ideas and suggestions. Such issues will be answered.
2. You cannot create issues to place any other questions. Such issues will not be answered but closed/deleted without any further warnings or replies.
3. If you continue on behaviour breaking these rules you will be reported to GitHub, MultiLinter repo can be deleted, extension on VS MarketPlace can be deleted, all to protect my reputation against bad users and bad reviews.

**If you are not comfortable with the above clarifications and warnings feel free to move on and do not bother me. Search for another extension, write your own, but that's it. No other questions will be answered.**

#### Notice for old time MultiLinter users
If you installed MultiLinter before November 16th, 2019 you'll get no further updates. To regain updates please uninstall and reinstall the extension.

#### How to configure it?
MultiLinter has few options in VS2019. You'll find a MultiLinter page in the VisualStudio preferences. It allows you to:

1. Enable a verbose debug window to find some configuration error.
2. Switch linting time. You can lint the file at save time or in real time (with favourite delay).
3. Enable multiple linting. Yes! You can lint same file with several linters, if you want.

First step is to configure it by editing the default config file which is placed (usually) in "%USERPROFILE%\\.multilinterrc.json" path. This is a Json file which overrides the internal configuration you can find here in repository. That file is in this repo to allow you to read and inherit.

Usually you need to override at least three properties for preconfigured linters, by this way:

`
{ "eslint": { enable: true, additionalArguments: "", fileExtensions: "js" }
`

It enables the eslint linter with no additional arguments other than the required ones and enables it to be used on .js files. Inherited internal config will provide all other settings to make eslint work.

MultiLinter allows only to interface VS2019 to Node.js linters. It does not install Node.js or linters.

**You must set up the environment by properly installing Node.js and your favorite linters in global or local mode in your project. Then, you must create a MultiLinter config file to enable linters on needed file extensions**.
**If you are using linters in global mode be sure that $PATH% env var contains the right path to access global npm folder**
**You should also disable internal VS2019 linting**.

#### Can I use only the preconfigured linters?
The answer is **no**. If you add new linters in your json configuration file you can use other ones. This requires to understand each json property and a bit of troubleshooting. See advanced section for this.

#### What is multiple linting?
If you enables multiple linting in VisualStudio preferences page and associates two or more linters to a single file extension MultiLinter will lint that files with every linter and will show you all results in errors windows of VS2019. This is disabled by default. Enable it in MultiLinter page of VisualStudio preferences.

#### Where to place MultiLinter configuration file?
Configuration file is found in same ways Node.js linters do. Search starts from the directory where is placed the file to be lint and then up to parent till the disk root. Last resort to find it is in %USERPROFILE%.

The configuration file must be named ".multilinterrc.json" or ".multilinterrc", same way as several linters.

Usually You can place it in %USERPROFILE%, which is last resort to find it.

#### Notes on local usage
You can use npm global installed linters or local installed linters. If you are using local linters and "Real Time" linting is enabled in VisualStudio preferences page, MultiLinter will creates a shadow file named [fileName].multilinter.[fileExtension] in same directory of the original file every time it needs to lint the document you're editing. The shadow file will be deleted as soon as linting is done. The shadow file can appear for a moment in Visual Studio Explorer. To avoid these files to be shown in Visual Studio Explorer add these lines to your project file (.csproj):

```xml
<ItemGroup>
  <None Remove="**\*.multilinter.*" Visible="false" />
  <Content Remove="**\*.multilinter.*" Visible="false" />
  <Compile Remove="**\*.multilinter.*" Visible="false" />
  <EmbeddedResource Remove="**\*.multilinter.*" Visible="false" />
</ItemGroup>
```

#### Advanced
You can modify behaviour of MultiLinter, enable or disable preconfigured linters or add new ones by changing its json configuration.

Json config file is a list of linters which overrides the default config (see config.json in repository for the base one).

Each property in json allows you to call the linter executable in a way it will return json result and extract warnings and errors from that json file by using right selectors.
