---
title: Warning Task | Microsoft Docs
description: Learn how MSBuild uses the Warning task to log a warning during a build based on an evaluated conditional statement.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Warning
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Warning task [MSBuild]
- MSBuild, Warning task
ms.assetid: 96ba5507-8b43-4f54-a1d7-9b15644dd56c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
---
# Warning task

Logs a warning during a build based on an evaluated conditional statement.

## Parameters

 The following table describes the parameters of the `Warning` task.

| Parameter | Description |
|---------------| - |
| `Code` | Optional `String` parameter.<br /><br /> The warning code to associate with the warning. |
| `File` | Optional `String` parameter.<br /><br /> Specifies the relevant file, if any. If no file is provided, the file containing the Warning task is used. |
| `HelpKeyword` | Optional `String` parameter.<br /><br /> The Help keyword to associate with the warning. |
| `Text` | Optional `String` parameter.<br /><br /> The warning text that MSBuild logs if the `Condition` parameter evaluates to `true`. |

## Remarks

 The `Warning` task allows MSBuild projects to check for the presence of a required configuration or property before proceeding with the next build step.

 If the `Condition` parameter of the `Warning` task evaluates to `true`, the value of the `Text` parameter is logged and the build continues to execute. If a `Condition` parameter does not exist, the warning text is logged. For more information on logging, see [Obtain build logs](../msbuild/obtaining-build-logs-with-msbuild.md).

 In addition to the parameters listed above, this task inherits parameters from the <xref:Microsoft.Build.Tasks.TaskExtension> class, which itself inherits from the <xref:Microsoft.Build.Utilities.Task> class. For a list of these additional parameters and their descriptions, see [TaskExtension base class](../msbuild/taskextension-base-class.md).

## Example

 The following code example checks for properties that are set on the command line. If there are no properties set, the project raises a warning event, and logs the value of the `Text` parameter of the `Warning` task.

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="ValidateCommandLine">
        <Warning
            Text=" The 0 property was not set on the command line."
            Condition="'$(0)' == ''" />
        <Warning
            Text=" The FREEBUILD property was not set on the command line."
            Condition="'$(FREEBUILD)' == ''" />
    </Target>
    ...
</Project>
```

## See also

- [Obtain build logs](../msbuild/obtaining-build-logs-with-msbuild.md)
- [Project file schema reference](../msbuild/msbuild-project-file-schema-reference.md)
