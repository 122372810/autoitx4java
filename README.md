#AutoItX4Java

[AutoIt](http://www.autoitscript.com/autoit3/index.shtml) is a very useful automation scripting language for Microsoft Windows. It allows for GUI automation using a very simple syntax and can be useful for testing Windows applications. It is packaged with AutoItX which supports accessing AutoIt functions through COM objects.

AutoItX4Java uses [JACOB](http://sourceforge.net/projects/jacob-project/) to access AutoItX through COM and strives to provide a native Java interface while maintaining the simplicity of AutoIt. Getting started is simple.

1. Download [JACOB](http://sourceforge.net/projects/jacob-project/).
2. Download and install [AutoIt](http://www.autoitscript.com/autoit3/index.shtml).
3. Add jacob.jar and autoitx4java.jar to your library path. Note that this project (autoitx4java.jar) is comprised of one code file so you can alternatively just include AutoItX.java in lieu of autoitx4java.jar.
4. Place the jacob-1.15-M4-x64.dll file in your library path.
5. Start using AutoItX. 

###Example
```
        File file = new File("lib", "jacob-1.15-M4-x64.dll"); //path to the jacob dll
        System.setProperty(LibraryLoader.JACOB_DLL_PATH, file.getAbsolutePath());
/**
添加记事本
*/
        AutoItX x = new AutoItX();
    String notepad = "无标题 - 记事本";
    String testString = "this is a test.";
    x.run("notepad.exe","",AutoItX.SW_SHOW);
    x.winActivate(notepad);
    x.winWaitActive(notepad);
    x.send(testString);
//    Assert.assertTrue(x.winExists(notepad, testString));
    x.winClose(notepad, testString);
    x.winWaitActive("记事本");
    x.send("{ALT}n");
//    Assert.assertFalse(x.winExists(notepad, testString));

/**
 * 	上传文件
 */

	File file = new File("lib","jacob-1.19-x64.dll");
	System.setProperty(LibraryLoader.JACOB_DLL_PATH, file.getAbsolutePath());
	
    AutoItX x = new AutoItX();

    x.winActivate("打开");//打开代表程序title
    x.winWaitActive("打开");
    x.controlSend("打开", "", "Edit1", "D:\\Desktop\\timg.jpg");//Edit1代表ClassnameNN
    try {
		Thread.sleep(3000);
	} catch (InterruptedException e1) {
		// TODO 自动生成的 catch 块
		e1.printStackTrace();
	}
    x.controlClick("打开", "", "1");

```

####Troubleshooting

Both AutoItX3 and Jacob dll's come in x86 and x64 versions. Ensure you use the correct dlls.

If AutoItX isn't disposing itself properly make a call to ComThread.Release() when you are done using AutoItX.
Refer to JACOB documentation: [JacobThreading](http://danadler.com/jacob/JacobThreading.html) and [Object Lifetime](http://danadler.com/jacob/JacobComLifetime.html)

####Note 

If you do not want to install AutoIt, you can just grab AutoItX3.dll and register it with: regsvr32.exe AutoItX3.dll

AutoItX4Java is comprised of one file so you can either use the jar or copy the .java file into your source.

If you get errors like: "Can’t co-create object" then ensure you have the AuotItX dll registered. If you need to manually register the 64 bit version, use: "\Windows\SysWOW64\regsvr32.exe AutoItX3_x64.dll" otherwise use "regsrv32.exe AutoItX3.dll".

####Warning

AutoItX4Java is not completely tested. Use at your own risk. 
