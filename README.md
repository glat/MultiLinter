# MultiLinter
VisualStudio multiple and customizable linting and formatting made easy

#### Short Description
MultiLinter allows you to use in VS2019 several standard linters and formatters available by Node.js such as (but not only) ESLint, JSLint, JSHint, Stylelint, CssLint, sass-lint, prettier, beautify.

#### Why Multilinter?
It was born because the linting integrated in VS2019 is now old. It features old version of linters and no way to change them.

#### Some clarifications

Some GitHub users tryied to stop MultiLinter development placing bad reviews on the VS MarketPlace and bothering me on this repo with questions I do not want to answer to, so, to be clear here are some clarifications about those questions:

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

#### Changelog

**v1.0.44**: Workaround to avoid bug (see https://github.com/stylelint/stylelint/issues/5122).

**v1.0.42**: Implemented formatters. Preconfigured are Prettier and Beautify. Can be present some bugs.

**v1.0.40**: Tested extension updating on VS MarketPlace.

**v1.0.35**: Implemented stdin usage for linters who support it (eslint and stylelint). Other linters in Real Time mode will continue to use a shadow copy of buffer on disk.

**v1.0.34**: New born of MultiLinter after attemped shutdown.

#### How to configure it?
MultiLinter has few options in VS2019. You'll find a MultiLinter page in the VisualStudio preferences. It allows you to:

1. Enable a verbose debug window to find some configuration error.
2. Switch linting time. You can lint the file at save time or in real time (with favourite delay).
3. Enable multiple linting. Yes! You can lint same file with several linters, if you want.
4. Switch formatting time. You can format the file manually (Use context menu on text or Visual Studio Edit Menu) or at save time.

First step is to configure it by editing the default config file which is placed (usually) in "%USERPROFILE%\\.multilinterrc.json" path. This is a Json file which overrides the internal configuration you can find here in repository. That file is in this repo to allow you to read and inherit.

Usually you need to override at least three properties for preconfigured linters, by this way:

```json
{
  "eslint": {
    "enabled": true,
    "additionalArguments": "",
    "fileExtensions": "js"
  }
}
```

It enables the eslint linter with no additional arguments other than the required ones and enables it to be used on .js files. Inherited internal config will provide all other settings to make eslint work.

MultiLinter allows only to interface VS2019 to Node.js linters and formatters. It does not install Node.js or linters/formatters.

**You must set up the environment by properly installing Node.js and your favorite linters/formatters in global or local mode in your project. Then, you must create a MultiLinter config file to enable linters/formatters on needed file extensions**.
**If you are using linters/formatters in global mode be sure that $PATH% env var contains the right path to access global npm folder**
**You should also disable internal VS2019 linting**.

#### Can I use only the preconfigured linters/formatters?
The answer is **no**. If you add new linters/formatters in your json configuration file you can use other ones. This requires to understand each json property and a bit of troubleshooting. See advanced section for this.

#### What is multiple linting?
If you enables multiple linting in VisualStudio preferences page and associates two or more linters to a single file extension MultiLinter will lint that files with every linter and will show you all results in errors windows of VS2019. This is disabled by default. Enable it in MultiLinter page of VisualStudio preferences.

#### What is multiple formatting?
Same as above for formatters. Of course it is not so much useful.

#### Where to place MultiLinter configuration file?
Configuration file is found in same ways Node.js linters/formatters do. Search starts from the directory where is placed the file to be linted/formatted and then up to parent till the disk root. Last resort to find it is in %USERPROFILE%.

The configuration file must be named ".multilinterrc.json" or ".multilinterrc", same way as several linters.

Usually You can place it in %USERPROFILE%, which is last resort to find it.

#### Notes on real time linting enabled
You can use npm global installed linters or local installed linters. If you are using a local installed linter and "Real Time" linting is enabled in VisualStudio preferences page, MultiLinter will use stdin to send data to the linter if it supports stdin input. In case linter does not support stdin usage MultiLinter will create a shadow file named [fileName].multilinter.[fileExtension] in same directory of the original file every time it needs to lint the document you're editing. The shadow file will be deleted as soon as linting is done. The shadow file can appear for a moment in Visual Studio Explorer. To avoid these files to be shown in Visual Studio Explorer add these lines to your project file (.csproj):

```xml
<ItemGroup>
  <None Remove="**\*.multilinter.*" Visible="false" />
  <Content Remove="**\*.multilinter.*" Visible="false" />
  <Compile Remove="**\*.multilinter.*" Visible="false" />
  <EmbeddedResource Remove="**\*.multilinter.*" Visible="false" />
</ItemGroup>
```

Linters who support stdin input are: **eslint** and **stylelint**. So, if you are using **only** eslint and stylelint you do **not** need to insert the above lines in your .csproj file. If you're using even one of the other integrated linter (jslint,jshint,csslint,sass-lint) you need to.

#### Notes on formatters

MultiLinter needs to format a file within the editor, so formatters must support stdin/stdout to be formatted. Integrated formatters are Prettier and Beautify. They support stdin/stdout.

#### Advanced
You can modify behaviour of MultiLinter, enable or disable preconfigured linters or add new ones by changing its json configuration.

Json config file is a list of linters which overrides the default config (see config.json in repository for the base one).

Each property in json allows you to call the linter executable in a way it will return json result and extract warnings and errors from that json file by using right selectors.
