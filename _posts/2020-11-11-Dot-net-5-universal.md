---
title: Microsoft publishes .NET 5 with the intention of unifying Mac, Windows, and Linux
layout: post
image: https://i.imgur.com/V88lXUE.png
tags: Microsoft
permalink: /microsoft-dot-net-5
---

Microsoft has announced the publication of .NET 5, the latest version of its well-known framework oriented to software development that over time has covered much more than the Windows operating system.

In the [Microsoft developer's blog](https://devblogs.microsoft.com/dotnet/announcing-net-5-0/), we are once again informed of the changes and new features introduced, which are usually quite numerous in each major version. Delving into the details, in .NET 5 we find improvements on several fronts, such as the performance of many components of the framework, in the languages C # 9 and F # 5, the performance of some libraries for JSON serialization and deployment options, in addition to having expanded the approach to Windows for ARM64 and WebAssembly.

It appears that Microsoft is attempting to provide a more homogeneous platform for the various supported systems with .NET: "NET 5.0 has a platform support matrix that is almost identical to .NET Core 3.1 for Windows, MacOS, and Linux. If you are using .NET Core 3.1 on a supported operating system, you should be able to adopt .NET 5.0 on that same version of the operating system for the most part. The most important addition to .NET 5.0 is Windows ARM64. The value to you is that you will be able to use a single set of APIs, languages, and tools to target a wide range of application types, including mobile, cloud, desktop, and IoT devices.

The Redmond giant has begun the journey by building .NET 5 "to allow a much larger group of developers to migrate their code and applications from the .NET Framework to .NET 5.0. We also did much of the initial work on 5.0 so that Xamarin developers can use the unified .NET platform when we launch .NET 6.0. This suggests that the process of integrating Mono into .NET may have begun, since Xamarin, the company in charge of Mono and its commercial implementation Xamarin, belongs to Microsoft.

NET 5 not only covers server level things, but also exclusive Windows components such as Windows Forms. Regarding Linux, which is what interests us in this portal, we have incorporated multiplatform support for 'System.DirectoryServices.Protocols', which was already present in Windows, but not in Linux and macOS. "'System.DirectoryServices.Protocols' is a lower level API than 'System.DirectoryServices' and enables (or can be used to enable) more scenarios. System.DirectoryServices' includes concepts/implementations only for Windows, so it was not an obvious choice to make it cross-platform. Both sets of APIs allow you to control and interact with a directory services server, such as LDAP or Active Directory.

For those who want to know all the details of .NET 5, please see the official announcement. The implementation for Linux, which is .NET Core, can be obtained from the corresponding web page for installation instructions. There is also a version in Docker container format.
