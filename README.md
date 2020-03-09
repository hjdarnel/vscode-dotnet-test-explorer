# .NET Core Test Explorer

This is a fork of [formulahendry/vscode-dotnet-test-explorer](https://github.com/formulahendry/vscode-dotnet-test-explorer), which I intend to release individual and keep up to date with that repo.

## Features

* Test Explorer for .NET Core

## Prerequisites

* [.NET Core](https://www.microsoft.com/net/core) is installed
* NUnit and MSTest requires a dotnet [sdk](https://www.microsoft.com/net/download) version of >= 2.2.104 and running dotnet tooling in English (see [#77](https://github.com/formulahendry/vscode-dotnet-test-explorer/issues/77) for details).

## New in 0.7.1

* Code lens symbols are displayed on the code lens row itself and not above
* To make it easier to see what the extension logs and what the test runner logs the logs for the test runner has been moved to a new output logger called Test explorer (Test runner output)

## Usage

Open a .NET Core test project, or set `dotnet-test-explorer.testProjectPath` to the folder path of .NET Core test project. Then, you will see all the tests in Test Explorer.

![test-explorer](images/test-explorer-065.gif)

By utilizing auto watch (see settings) test can be run upon changing in files.

![test-explorer](images/test-explorer-065-autowatch.gif)

#### Configuring multiple test projects

Setting dotnet-test-explorer.testProjectPath accepts a glob pattern that should point to your test directories. You can also point to files and it will figure out the corresponding path.

Given the folder structure
* root
  * testProjectOne
    * testproject1.Tests.csproj
  * testProjectTwo
    * testproject2.Tests.csproj

the glob pattern "+(testProjectOne|testProjectTwo)" or "**/*Tests.csproj" should add both of the test projects.

Due to some performance concerns discovery and test running over multiple directories are run one at a time in a synchronous fashion. When running specific tests (eg, not running all tests) the extension should be smart enough to figure out which test directory should be run and only run tests for that directory.

#### Debugging

To debug a test, right click the test and choose to Debug test. The option to run and debug test that appear in the code lens are provided by the omnisharp plugin and has nothing to do with this extension.

The debugger might get stuck before loading your test assembly code. If this happens you can continue the debug process (F5) and it should load the rest of the assemblies and stop and the desired breakpoint.

#### Stopping the current test runner(s)

Press the stop button in the top menu. After killing the process(es) it will perform a new test discovery. This also works as a reset of sorts so if the extension has managed to end up in a weird state where it thinks a test is running even though it is not or that the debugger is running even though it is not the stop button can solve these types of issues as well.

![test-explorer](images/stop.PNG)

#### Logging

Text from the dotnet test output as well as debug info is written to the Output/Test explorer terminal window. To view the log you can access it simply by clicking the view log icon.

![showlog](images/showlog.png)


## Keyboard shortcuts

* Run all tests, default Alt+R Alt+A

* Rerun last command, default Alt+R Alt+R

* Run test(s) in context, default Alt+R Alt+C

## Settings

* `dotnet-test-explorer.testProjectPath`: Glob pattern that points to path of .NET Core test project(s). (Default is **""**)
* `dotnet-test-explorer.useTreeView`: If false, will list all tests as the full namespace. When set to true a tree will be created based on the namespaces of the tests. (Default is **true**)
* `dotnet-test-explorer.showCodeLens`: Determines whether to show the CodeLens test status or not. (Default is **true**)
* `dotnet-test-explorer.codeLensFailed`: The text to display in the code lens when a test has failed. (Default is **""**)
* `dotnet-test-explorer.codeLensPassed`: The text to display in the code lens when a test has passed. (Default is **""**)
* `dotnet-test-explorer.codeLensSkipped`: The text to display in the code lens when a test has been skipped. (Default is **""**)
* `dotnet-test-explorer.pathForResultFile`: The path to (temporarily) store test result files in. (Default is OS temp dir)
* `dotnet-test-explorer.autoExpandTree`: If true, the tree will be in an expanded state by default. (Default is **false**)
* `dotnet-test-explorer.addProblems`: If true, failed tests will add to problems view. (Default is **true**)
* `dotnet-test-explorer.autoWatch`: If true, starts dotnet watch test after test discovery is completed. (Default is **false**)
* `dotnet-test-explorer.testArguments`: Additional arguments that are added to the dotnet test command
* `dotnet-test-explorer.leftClickAction`: What happens when a test in the list is left clicked. (Default is **gotoTest**)
* `dotnet-test-explorer.runInParallel`: If true, will discover/build and run test in parallel if you have multiple test projects (Default is **false**)

## Known issues
##### Go to test does not work with multiple workspaces
This is because of limitations in the omnisharp extensions. We can only navigate to symbols which are in the currently selected workspace.

##### Test result is not shown in CodeLens / tree
Try and change the setting dotnet-test-explorer.pathForResultFile to point to a folder you have access right too. CodeLens functionality also requires the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp))

##### No tree view or color coded explorer for NUnit / MSTest
This requires you to run dotnet SDK version 2.2.104 or higher. The extension tries to run the commands with the English cli but if things are not working as expected anyway it may be due to the cli language (see [#77](https://github.com/formulahendry/vscode-dotnet-test-explorer/issues/77) for details).

##### xUnit projects assembly name needs to match the test class namespace
See [#201](https://github.com/formulahendry/vscode-dotnet-test-explorer/issues/201)

##### DisplayName attribute not working for xUnit
See [#56](https://github.com/formulahendry/vscode-dotnet-test-explorer/issues/56)

##### Project discovery with UNC Paths doesn't work
See [#179](https://github.com/formulahendry/vscode-dotnet-test-explorer/issues/179)

## Telemetry data

By default, anonymous telemetry data collection is turned on to understand user behavior to improve this extension. To disable it, update the settings.json as below:
```json
{
    "dotnet-test-explorer.enableTelemetry": false
}
```

## Change Log

See Change Log [here](CHANGELOG.md)

## Issues

If you find any bug or have any suggestion/feature request, please submit the [issues](https://github.com/hjdarnel/vscode-dotnet-test-explorer/issues) to the GitHub Repo.

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):
<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/stefanforsberg"><img src="https://avatars1.githubusercontent.com/u/358570?v=4" width="100px;" alt=""/><br /><sub><b>Stefan Forsberg</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=stefanforsberg" title="Code">💻</a></td>
    <td align="center"><a href="https://www.zhihu.com/people/formulahendry"><img src="https://avatars0.githubusercontent.com/u/1050213?v=4" width="100px;" alt=""/><br /><sub><b>Jun Han</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=formulahendry" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/jmansar"><img src="https://avatars2.githubusercontent.com/u/101620?v=4" width="100px;" alt=""/><br /><sub><b>Jerzy Mansarliński</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=jmansar" title="Code">💻</a></td>
    <td align="center"><a href="http://darnell.io"><img src="https://avatars1.githubusercontent.com/u/7868899?v=4" width="100px;" alt=""/><br /><sub><b>Henry Darnell</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=hjdarnel" title="Code">💻</a> <a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=hjdarnel" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/Mgenuit"><img src="https://avatars3.githubusercontent.com/u/42111466?v=4" width="100px;" alt=""/><br /><sub><b>Mgenuit</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=Mgenuit" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/DTeuchert"><img src="https://avatars2.githubusercontent.com/u/16237337?v=4" width="100px;" alt=""/><br /><sub><b>DTeuchert</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=DTeuchert" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/seesharper"><img src="https://avatars0.githubusercontent.com/u/1034073?v=4" width="100px;" alt=""/><br /><sub><b>Bernhard Richter</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=seesharper" title="Code">💻</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://www.janaka.co.uk"><img src="https://avatars0.githubusercontent.com/u/51779?v=4" width="100px;" alt=""/><br /><sub><b>Janaka Abeywardhana</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=janaka" title="Code">💻</a></td>
    <td align="center"><a href="http://stapp.space"><img src="https://avatars2.githubusercontent.com/u/2411329?v=4" width="100px;" alt=""/><br /><sub><b>Piotr Stapp</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=ptrstpp950" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/teamdynamiq"><img src="https://avatars0.githubusercontent.com/u/34121425?v=4" width="100px;" alt=""/><br /><sub><b>teamdynamiq</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=teamdynamiq" title="Code">💻</a></td>
    <td align="center"><a href="http://www.doctran.co.uk"><img src="https://avatars1.githubusercontent.com/u/10943153?v=4" width="100px;" alt=""/><br /><sub><b>Chris</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=CPardi" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/ciel"><img src="https://avatars1.githubusercontent.com/u/438196?v=4" width="100px;" alt=""/><br /><sub><b>Ciel</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=ciel" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/davidpendraykalibrate"><img src="https://avatars2.githubusercontent.com/u/35926989?v=4" width="100px;" alt=""/><br /><sub><b>David Pendray</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=davidpendraykalibrate" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/Jjagg"><img src="https://avatars0.githubusercontent.com/u/14875382?v=4" width="100px;" alt=""/><br /><sub><b>Jesse</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=Jjagg" title="Code">💻</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/Tarmil"><img src="https://avatars0.githubusercontent.com/u/921395?v=4" width="100px;" alt=""/><br /><sub><b>Loïc Denuzière</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=Tarmil" title="Code">💻</a></td>
    <td align="center"><a href="http://blogorama.nerdworks.in/"><img src="https://avatars1.githubusercontent.com/u/628128?v=4" width="100px;" alt=""/><br /><sub><b>Rajasekharan Vengalil</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=avranju" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/rhyswat"><img src="https://avatars2.githubusercontent.com/u/1647341?v=4" width="100px;" alt=""/><br /><sub><b>Rhys Watkin</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=rhyswat" title="Code">💻</a></td>
    <td align="center"><a href="http://samcragg.wordpress.com/"><img src="https://avatars2.githubusercontent.com/u/1365438?v=4" width="100px;" alt=""/><br /><sub><b>Samuel Cragg</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=samcragg" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/sandy081"><img src="https://avatars2.githubusercontent.com/u/10746682?v=4" width="100px;" alt=""/><br /><sub><b>Sandeep Somavarapu</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=sandy081" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/tiagodenoronha"><img src="https://avatars2.githubusercontent.com/u/27889458?v=4" width="100px;" alt=""/><br /><sub><b>Tiago Noronha</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=tiagodenoronha" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/alexriedl"><img src="https://avatars3.githubusercontent.com/u/6668240?v=4" width="100px;" alt=""/><br /><sub><b>alexriedl</b></sub></a><br /><a href="https://github.com/hjdarnel/vscode-dotnet-test-explorer/commits?author=alexriedl" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!