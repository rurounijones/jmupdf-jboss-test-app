# Overview

This is a tiny jsp application for testing the jboss-jmupdf-module located [here](https://github.com/rurounijones/jmupdf-jboss-module)

You should make sure that that module is installed in your JBoss AS7 server before running this application.

Create a WAR file using

    jar -cvf test.war *.jsp WEB-INF

Then copy to the deployments folder of your JBoss AS7 installation.

Access the page using http://yourjbossurl/test/test.jsp

If the page loads without trouble then all is good, if there are errors then this is not good.

## Current status

The application contains the required jar and native library files to work in the WEB-INF/lib directory. With these files present
the page displays correctly.

However we want this application to work without the files in WEB-INF/lib since they should not be needed. Instead the app should be
able to use the global module mentioned earlier by reading jboss-deployment-structure.xml.

To do this delete (or move) the WEB-INF/lib directory so that it is no longer included in the WAR, re-create the WAR and re-deploy

The page will fail to load with the following error:

```
An error occurred at line: 6 in the generated java file
Only a type can be imported. com.jmupdf.exceptions.DocException resolves to a package

An error occurred at line: 7 in the generated java file
Only a type can be imported. com.jmupdf.exceptions.DocSecurityException resolves to a package

An error occurred at line: 8 in the generated java file
Only a type can be imported. com.jmupdf.pdf.PdfDocument resolves to a package

Stacktrace:
	org.apache.jasper.compiler.DefaultErrorHandler.javacError(DefaultErrorHandler.java:92)
	org.apache.jasper.compiler.ErrorDispatcher.javacError(ErrorDispatcher.java:330)
	org.apache.jasper.compiler.JDTCompiler.generateClass(JDTCompiler.java:446)
	org.apache.jasper.compiler.Compiler.compile(Compiler.java:362)
	org.apache.jasper.compiler.Compiler.compile(Compiler.java:340)
	org.apache.jasper.compiler.Compiler.compile(Compiler.java:327)
	org.apache.jasper.JspCompilationContext.compile(JspCompilationContext.java:607)
	org.apache.jasper.servlet.JspServletWrapper.service(JspServletWrapper.java:312)
	org.apache.jasper.servlet.JspServlet.serviceJspFile(JspServlet.java:326)
	org.apache.jasper.servlet.JspServlet.service(JspServlet.java:253)
	javax.servlet.http.HttpServlet.service(HttpServlet.java:847)

```

Which, as far as I know, means that the application is not loading the global module for some reason.

This has been tested on a Windows 2008 R2 Standard server JBoss installation

## Help!

Any help to get this application working would be appreciated. I believe it is a configuration issue either in this application or
(more likely) in the configuration of the global module.





