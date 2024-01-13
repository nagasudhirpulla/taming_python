# Static file hosting with directory browsing in IIS

  

Date Created: December 28, 2023 10:29 AM

Status: Doing

  

## What is static file hosting

  

- Files in the server folder can be served over HTTP based on the URL. (Example: http://localhost/sample.txt)

  

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

## What is directory browsing

  

- The server folder contents can be viewed and navigated in a web browser over HTTP

  

## Use cases of static file hosting with directory browsing

  

- Users can just view and download the server folder contents but cannot upload, delete or modify the server contents

- File transfer can be facilitated over HTTP instead of SMB or other file sharing protocols

  

## Why use IIS for static file hosting

  

- IIS is a production ready web server for Windows OS

- IIS can be configured conveniently with both GUI and command line

- Security features like limiting access to file extensions, file download limit, URL length restriction etc can be done easily using Request filtering IIS module

  

## Install IIS from UI in Windows

  

- For desktop, open “Turn Windows features On or Off”

- For Servers, open Server Manager and click on **Add Roles and Features** in the **Manage** menu

- Expand the Internet Information Services and select the following for basic static hosting in IIS

- [IIS Management Console](https://learn.microsoft.com/en-us/iis/get-started/getting-started-with-iis/getting-started-with-the-iis-manager-in-iis-7-and-iis-8) - IIS Manager application for managing websites via user interface

- [Default Document](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/defaultdocument/) - Serve default document if file name is not mentioned

- [Directory browsing](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/directorybrowse) - Allow users to view and download server folder contents in the browser

- [HTTP Logging](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/httplogging) - Configure logging for website

- [Static Content Compression](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/httpcompression/) - Compress and serve static content for faster delivery

- [Request Filtering](https://learn.microsoft.com/en-us/iis/manage/configuring-security/configure-request-filtering-in-iis) - restrict requests based on the HTTP verbs, file extensions, content length, URL length, query string length etc

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

## Install IIS from command line

  

```bash

Start /w pkgmgr /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel

```

  

## Host a folder in IIS

  

- Select a folder to be hosted in IIS

- Create a file named web.config in the hosted folder with the following content. This will enable directory browsing feature so that the users can view the hosted folder contents

  

```xml

<?xml version="1.0" encoding="UTF-8"?>

<configuration>

<system.webServer>

<directoryBrowse enabled="true" />

</system.webServer>

</configuration>

```

  

- Right click on the hosted folder and open the Properties dialog. Under the security tab, make sure that the user named “IUSR” and the user group “IIS_IUSRS” has the permissions Read & execute, List folder contents, Read.

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/IIS)

  

- Open IIS Manager. In the left pane, Right click on the Sites folder and create a new website. Select the desired server port, folder path as shown below

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

- After creating the website, it will shown in the left pane of IIS under sites folder. The site can be started or stopped or opened in browser using “Manage Website” menu as shown below. The folder of the website can be opened in file explorer using the “Explore” menu

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

- If the website is configured correctly, the folder can be viewed in the web browser as shown below

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

## Default document setting

  

- Directory listing will not be shown if any file with any one default document name is present in the folder. For example, if a file named index.html is present in the folder, the file will be displayed instead of the folder contents

- Default document is a desired website feature in most of the cases especially when hosting a website.

- But for hosting a directory browsing website, default document feature may not be required

- To configure default document setting for a website, select the website and double “Default Document” icon as shown below

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

- Default document feature can be disabled or the default document names along with priority can be configured as shown below

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

## Request filtering module for rule based restrictions

  

- Request Filtering module can be used to restrict file downloads based on configurable rules.

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

- File extensions, HTTP verbs, file content length, query string length, URL length can be configured to limit the type of files downloadable to the users as shown below.

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

## Directory browsing with sorting and extra columns using aspx

  

- Instead of IIS built in directory listing, the folder contents can be rendered as an interactive HTML table with column sorting and extra columns as shown below using aspx server-side scripting. The table sorting is done using JavaScript on the client side. Hence page is not reloaded every time sorting is changed. Also the folder contents are sorted on date by default instead of sorting on filename. Files will be opened in new tab upon clicking on them. Folder or Files marked hidden are also not shown.

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

- To enable aspx rendering in IIS websites, ensure ASP.NET latest version is enabled in windows features as shown below

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

- Paste the two files files `Files.aspx` and `Files.aspx.cs` in the server folder.

  

```csharp

// Files.aspx.cs

using System;

using System.IO;

using System.Web;

using System.Collections.Generic;

  

namespace Files

{

public partial class FilesPage : System.Web.UI.Page

{

public DirectoryListingEntryCollection listing = new DirectoryListingEntryCollection();

public string path = "/";

protected void Page_Load()

{

path = Request.QueryString["path"];

if (string.IsNullOrEmpty(path))

{

path = "/";

}

else

{

path = VirtualPathUtility.AppendTrailingSlash(path);

}

  

string sortBy = Request.QueryString["sortby"];

  

//

// Databind to the directory listing

//

DirectoryInfo dirInfo = new DirectoryInfo(Server.MapPath(path));

FileSystemInfo[] fiFiles = dirInfo.GetFileSystemInfos();

foreach (FileSystemInfo f in fiFiles)

{

if (f.Attributes.HasFlag(FileAttributes.Hidden)) { continue; }

DirectoryListingEntry e = new DirectoryListingEntry();

e.FileSystemInfo = f;

e.Filename = f.Name;

//e.Path = f.FullName;

e.VirtualPath = path + (path.EndsWith("/") ? "" : "/") + f.Name;

listing.Add(e);

}

  

if (listing == null)

{

throw new Exception("This page cannot be used without the DirectoryListing module");

}

  

//

// Handle sorting

//

if (string.IsNullOrEmpty(sortBy))

{

// set default sorting

sortBy = "daterev";

}

  

if (sortBy.Equals("name"))

{

listing.Sort(DirectoryListingEntry.CompareFileNames);

}

else if (sortBy.Equals("namerev"))

{

listing.Sort(DirectoryListingEntry.CompareFileNamesReverse);

}

else if (sortBy.Equals("date"))

{

listing.Sort(DirectoryListingEntry.CompareDatesModified);

}

else if (sortBy.Equals("daterev"))

{

listing.Sort(DirectoryListingEntry.CompareDatesModifiedReverse);

}

else if (sortBy.Equals("size"))

{

listing.Sort(DirectoryListingEntry.CompareFileSizes);

}

else if (sortBy.Equals("sizerev"))

{

listing.Sort(DirectoryListingEntry.CompareFileSizesReverse);

}

  

//

// Prepare the file counter label

//

FileCount.Text = listing.Count + " items";

  

//

//

// Parepare the parent path label

string parentPath = null;

if (path.Equals("/") || path.Equals(VirtualPathUtility.AppendTrailingSlash(HttpRuntime.AppDomainAppVirtualPath)))

{

// cannot exit above the site root or application root

parentPath = null;

}

else

{

parentPath = VirtualPathUtility.Combine(path, "..");

}

  

if (string.IsNullOrEmpty(parentPath))

{

NavigateUpLink.Visible = false;

NavigateUpLink.Enabled = false;

}

else

{

NavigateUpLink.NavigateUrl = "?path=" + parentPath;

}

}

  

public string GetFileSizeString(FileSystemInfo info)

{

if (info is FileInfo)

{

return string.Format("{0}", (int)(((FileInfo)info).Length * 10 / (double)1024) / (double)10);

}

else

{

return string.Empty;

}

}

}

  

public class DirectoryListingEntryCollection : List<DirectoryListingEntry>

{

}

  

public class DirectoryListingEntry

{

//public string Path;

public string VirtualPath;

public string Filename;

public FileSystemInfo FileSystemInfo;

  

internal static int CompareFileNames(DirectoryListingEntry x, DirectoryListingEntry y)

{

return x.Filename.CompareTo(y.Filename);

}

  

internal static int CompareFileNamesReverse(DirectoryListingEntry x, DirectoryListingEntry y)

{

return -1 * x.Filename.CompareTo(y.Filename);

}

  

internal static int CompareDatesModified(DirectoryListingEntry x, DirectoryListingEntry y)

{

return x.FileSystemInfo.LastWriteTime.CompareTo(y.FileSystemInfo.LastWriteTime);

}

  

internal static int CompareDatesModifiedReverse(DirectoryListingEntry x, DirectoryListingEntry y)

{

return -1 * x.FileSystemInfo.LastWriteTime.CompareTo(y.FileSystemInfo.LastWriteTime);

}

  

internal static int CompareFileSizes(DirectoryListingEntry x, DirectoryListingEntry y)

{

if (x.FileSystemInfo is DirectoryInfo)

{

return -1;

}

if (y.FileSystemInfo is DirectoryInfo)

{

return 1;

}

return ((FileInfo)x.FileSystemInfo).Length.CompareTo(((FileInfo)y.FileSystemInfo).Length);

}

  

internal static int CompareFileSizesReverse(DirectoryListingEntry x, DirectoryListingEntry y)

{

if (x.FileSystemInfo is DirectoryInfo)

{

return -1;

}

if (y.FileSystemInfo is DirectoryInfo)

{

return 1;

}

return -1 * ((FileInfo)x.FileSystemInfo).Length.CompareTo(((FileInfo)y.FileSystemInfo).Length);

}

  

}

}

```

  

```html

<!-- Files.aspx -->

<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Files.aspx.cs" Inherits="Files.FilesPage" %>

  

<%@ Import Namespace="System.Collections.Generic" %>

<%@ Import Namespace="System.IO" %>

<%@ Import Namespace="Files" %>

<!DOCTYPE html>

<html>

<head>

<title>Contents of <%= path %></title>

<style type="text/css">

a {

text-decoration: none;

}

  

a:hover {

text-decoration: underline;

}

  

p {

font-family: verdana;

font-size: 10pt;

}

  

h2 {

font-family: verdana;

}

  

td, th {

font-family: verdana;

font-size: 10pt;

padding-left: 1em;

}

  

th {

text-align: left;

text-decoration: underline;

}

</style>

</head>

<body>

<h2>

<asp:HyperLink runat="server" ID="NavigateUpLink">[To Parent Directory]</asp:HyperLink>

<%= path %>

</h2>

<hr />

<table>

<tr>

<th id="abcd">Name</th>

<th>Last Modified</th>

<th>Size (KB)</th>

<th>Extension</th>

<th>Type</th>

</tr>

<% foreach (DirectoryListingEntry fItem in listing)

{ %>

<tr>

<td>

<% if (fItem.FileSystemInfo is DirectoryInfo)

{%>

<a href="?path=<%=fItem.VirtualPath%>"><%=fItem.Filename%></a>

<%}

else

{%>

<a href="<%=fItem.VirtualPath%>" target="_blank"><%=fItem.Filename%></a>

<%}%>

</td>

<td><%= fItem.FileSystemInfo.LastWriteTime.ToString("yyyy-MMM-dd HH:mm")%></td>

<td><%= GetFileSizeString(fItem.FileSystemInfo) %></td>

<td><%=fItem.FileSystemInfo.Extension %></td>

<td><%=(fItem.FileSystemInfo is DirectoryInfo)?"folder":"file" %></td>

</tr>

<% } %>

</table>

  

<hr />

<p>

<asp:Label runat="Server" ID="FileCount" />

</p>

<script>

// https://stackoverflow.com/questions/14267781/sorting-html-table-with-javascript

var getCellValue = function (tr, idx) { return tr.children[idx].innerText || tr.children[idx].textContent; }

  

var comparer = function (idx, asc) {

return function (a, b) {

return function (v1, v2) {

return v1 !== '' && v2 !== '' && !isNaN(v1) && !isNaN(v2) ? v1 - v2 : v1.toString().localeCompare(v2);

}(getCellValue(asc ? a : b, idx), getCellValue(asc ? b : a, idx));

}

};

  

// wire up the table sorting feature

Array.prototype.slice.call(document.querySelectorAll('th')).forEach(function (th) {

th.addEventListener('click', function () {

var table = th.parentNode

while (table.tagName.toUpperCase() != 'TABLE') table = table.parentNode;

Array.prototype.slice.call(table.querySelectorAll('tr:nth-child(n+2)'))

.sort(comparer(Array.prototype.slice.call(th.parentNode.children).indexOf(th), this.asc = !this.asc))

.forEach(function (tr) { table.appendChild(tr) });

})

});

</script>

</body>

</html>

```

  

- Instead of opening `Files.aspx` explicitly in the URL, it can be configured as a default document as shown below

  

[Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/iis)

  

- Since we are using Files.aspx for rendering the directory contents, directory browsing feature in the website can be disabled if required.

- Now the aspx based directory browsing can be used for the website

  

## References

  

- [https://learn.microsoft.com/en-us/iis/manage/creating-websites/scenario-build-a-static-website-on-iis](https://learn.microsoft.com/en-us/iis/manage/creating-websites/scenario-build-a-static-website-on-iis)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTc5NDE5MDksLTk5Njk0NDE4MV19
-->