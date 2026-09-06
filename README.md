[![nuget](https://img.shields.io/nuget/v/OxyPlot.Avalonia.svg)](https://www.nuget.org/packages/OxyPlot.Avalonia) ![License](https://img.shields.io/github/license/oxyplot/oxyplot-avalonia.svg) ![Size](https://img.shields.io/github/repo-size/oxyplot/oxyplot-avalonia.svg)

# OxyPlot.Avalonia

> **Fork 说明（hebin123456/oxyplot-avalonia）**
>
> 本 fork 为 [ForkPlus-Next](https://github.com/hebin123456/ForkPlus-Next) 提供按 **Avalonia 12.1.1** 编译的
> OxyPlot.Avalonia 预编译 NuGet 包（上游 master 停留在 Avalonia 11.0.0，且官方仓库不产出 release 二进制）。
>
> - 包版本使用 `-avalonia12.x` 后缀（如 `2.1.2-avalonia12.1`），与 nuget.org 官方 2.1.2 区分，恢复时不会混淆。
> - 发布方式：push `v*` tag 触发 [release workflow](.github/workflows/release.yml)，构建出的
>   `OxyPlot.Avalonia.<版本>.nupkg` 自动挂到 GitHub Release。
> - 消费方式（ForkPlus-Next，与 tokei / biturbo 同模式）：构建期从本仓库 latest release 下载 nupkg
>   到本地 NuGet 源目录，通过 `PackageReference` 恢复。
> - 升级流程：改 `Source/Directory.Build.props` 的 `AvaloniaVersion` 与 csproj 的 `VersionPrefix`
>   → 提交 → 打 tag（如 `v2.1.2-avalonia12.2`）→ workflow 自动发版。

[OxyPlot](https://github.com/oxyplot) is a plotting library for .NET. This [package](https://www.nuget.org/packages/OxyPlot.Avalonia) targets Avalonia applications.

```
dotnet add package OxyPlot.Avalonia
```

### Usage

To use the library, add the following to your `App.xaml`:

```xml
<Application xmlns="https://github.com/avaloniaui"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             x:Class="Sensei.Presentation.Avalonia.App">
    <Application.Styles>
        <StyleInclude Source="avares://Avalonia.Themes.Default/DefaultTheme.xaml"/>
        <StyleInclude Source="avares://Avalonia.Themes.Default/Accents/BaseLight.xaml"/>
      
        <!-- Add the line below to get OxyPlot UI theme applied. -->
        <StyleInclude Source="resm:OxyPlot.Avalonia.Themes.Default.xaml?assembly=OxyPlot.Avalonia"/>
      
        <!-- Add the line below to get OxyPlot UI theme applied in Avalonia 11. -->
        <StyleInclude Source="avares://OxyPlot.Avalonia/Themes/Default.axaml"/>
    </Application.Styles>
</Application>
```

Then, you can add plots to your application, as such:

```xml
<avalonia:Plot Height="150" 
               PlotMargins="50 0 0 0"
               PlotAreaBorderColor="#999999">
    <avalonia:Plot.Series>
        <avalonia:AreaSeries 
            DataFieldX="Index"
            DataFieldY="Value"
            ItemsSource="{Binding Path=Values}"
            Color="#fd6d00" />
    </avalonia:Plot.Series>
</avalonia:Plot>
```

See the [AvaloniaExamples](https://github.com/oxyplot/oxyplot-avalonia/tree/master/Source/Examples/Avalonia/AvaloniaExamples) project and [OxyPlot Documentation](https://readthedocs.org/projects/oxyplot/downloads/pdf/latest/) to learn how to create more complex plots. 


### Installing Preview Versions

To access the latest version of `OxyPlot.Avalonia` you can add this repo as a [submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to your own git repo:

```sh
mkdir ./external
git submodule add git@github.com:oxyplot/oxyplot-avalonia.git ./external/oxyplot-avalonia
# Reference the ../external/oxyplot-avalonia/Source/OxyPlot.Avalonia/OxyPlot.Avalonia.csproj project then.
```

Another way is to import our [Azure Artifacts NuGet package feed](https://worldbeater.visualstudio.com/OxyPlot.Avalonia/_packaging) by creating the following `nuget.config` file:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <clear /> <!-- Add other external NuGet package sources here -->
    <add key="OxyPlot.Avalonia-CI" value="https://worldbeater.pkgs.visualstudio.com/OxyPlot.Avalonia/_packaging/OxyPlot.Avalonia-CI/nuget/v3/index.json" />
  </packageSources>
</configuration>
```

Next, install the latest preview version of the `OxyPlot.Avalonia` package as such:

```
dotnet add package OxyPlot.Avalonia
```
