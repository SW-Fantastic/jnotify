
# JNotify

this is a repository for a custom jnotify library which can load native library from anywhere you 
need.

* * *

JNotify works on Linux with INotify support (Tested on 2.6.14), Mac OS X 10.5 or
higher (Tested on 10.6.2), and on Windows XP/2K/NT (Tested on XP and on Windows 7).

You can test run JNotify with the command:
java -Djava.library.path=. -jar jnotify-0.94.jar [directory]
which will monitor the specified directory or the current directory if not specified and output events to the console.

To use JNotify, You will need to have the appropriate shared library in your java.library.path
Usage is very simple:

```
// to add a watch :
String path = "/home/omry/tmp";
int mask =  JNotify.FILE_CREATED | 
			JNotify.FILE_DELETED | 
			JNotify.FILE_MODIFIED| 
			JNotify.FILE_RENAMED;
boolean watchSubtree = true;
int watchID = JNotify.addWatch(path, mask, watchSubtree, new JNotifyListener()
{
	public void fileRenamed(int wd, String rootPath, String oldName, String newName)
	{
		System.out.println("JNotifyTest.fileRenamed() : wd #" + wd + " root = " + rootPath + ", " + oldName + " -> " + newName);
	}

	public void fileModified(int wd, String rootPath, String name)
	{
		System.out.println("JNotifyTest.fileModified() : wd #" + wd + " root = " + rootPath + ", " + name);
	}

	public void fileDeleted(int wd, String rootPath, String name)
	{
		System.out.println("JNotifyTest.fileDeleted() : wd #" + wd + " root = " + rootPath
				+ ", " + name);
	}

	public void fileCreated(int wd, String rootPath, String name)
	{
		System.out.println("JNotifyTest.fileCreated() : wd #" + wd + " root = " + rootPath
				+ ", " + name);
	}
});




// to remove watch:
boolean res = JNotify.removeWatch(watchID);
if (!res)
{
	// invalid watch ID specified.
}


```



