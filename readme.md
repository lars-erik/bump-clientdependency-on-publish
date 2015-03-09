## Bumping ClientDependency when you publish

The .pubxml files you use to publish websites with Visual Studio are actually msbuild files.  
This means we can run all kinds of nice msbuild tasks when we publish.  

To use this task to bump the ClientDependency version when you publish, all you have to do is include it in the pubxml file:

    <Import Project="BumpClientDependency.targets"/>

An example of a full pubxml file for deployment to disk:

    <?xml version="1.0" encoding="utf-8"?>
    <!--
    This file is used by the publish/package process of your Web project. You can customize the behavior of this process
    by editing this MSBuild file. In order to learn more about this please visit http://go.microsoft.com/fwlink/?LinkID=208121. 
    -->
    <Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <WebPublishMethod>FileSystem</WebPublishMethod>
        <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
        <LastUsedPlatform>Any CPU</LastUsedPlatform>
        <SiteUrlToLaunchAfterPublish />
        <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
        <ExcludeApp_Data>False</ExcludeApp_Data>
        <publishUrl>$(MSBuildThisFileDirectory)..\..\..\Disk Release</publishUrl>
        <DeleteExistingFiles>False</DeleteExistingFiles>
      </PropertyGroup>

      <Import Project="$(MSBuildThisFileDirectory)..\..\..\BumpClientDependency.targets"/>

    </Project>

The example has the targets file in the solution root.  
It uses the pubxml's directory as starting point for both publish url and the targets file.

The targets file is defaulted to where UmbracoCms has the ClientDependency configuration.  
You can change the path in the targets file, or override the property in your pubxml file:

    <Import Project="$(MSBuildThisFileDirectory)..\..\..\BumpClientDependency.targets"/>
    <PropertyGroup>
        <BumpFile>$(MSBuildThisFileDirectory)..\..\config\AlternativeClientDependency.config</BumpFile>
    </PropertyGroup>

Happy bumping! :)