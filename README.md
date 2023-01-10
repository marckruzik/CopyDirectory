# CopyDirectory
Copy a complete directory recursively in the most simple way.  
This is a nuget version of the official Microsoft code example to copy directories.

# Usage
```csharp
CopyDirectory.IO.CopyDirectory(sourceDir, destinationDir);
```

# Code

```csharp
public static void CopyDirectory(string sourceDir, string destinationDir, bool recursive=true)
{
    // Get information about the source directory
    var dir = new DirectoryInfo(sourceDir);

    // Check if the source directory exists
    if (!dir.Exists)
        throw new DirectoryNotFoundException($"Source directory not found: {dir.FullName}");

    // Cache directories before we start copying
    DirectoryInfo[] dirs = dir.GetDirectories();

    // Create the destination directory
    Directory.CreateDirectory(destinationDir);

    // Get the files in the source directory and copy to the destination directory
    foreach (FileInfo file in dir.GetFiles())
    {
        string targetFilePath = Path.Combine(destinationDir, file.Name);
        file.CopyTo(targetFilePath);
    }

    // If recursive and copying subdirectories, recursively call this method
    if (recursive)
    {
        foreach (DirectoryInfo subDir in dirs)
        {
            string newDestinationDir = Path.Combine(destinationDir, subDir.Name);
            CopyDirectory(subDir.FullName, newDestinationDir, true);
        }
    }
}
```

This code comes from Microsoft official documentation:

https://learn.microsoft.com/en-us/dotnet/standard/io/how-to-copy-directories

It is mostly unchanged (except the "public" access and the default "recursive=true").  
Nothing more, nothing less.

# FAQ
## Why this nuget?

This is no built-in function in C# to copy paste a directory. And there is no nuget to easily copy paste a directory.  
The usual way to go is to copy paste the code above, and put it somewhere in your code.  
So I made this nuget, so we can have an easy way to copy paste a directory.

## I will just copy paste the code like everyone does!
Feel free to do so.

## You did not see the XXX nuget which can copy paste folders!
Contact me or make a pull request, so I can write here a list of nugets which can copy paste folders (please describe their strong points).
