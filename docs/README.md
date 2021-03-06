# Standalone MultiScan Tools for ZAP (Zed Attack Proxy)
MultiscanTools is a set of security testing tools for ZAP: it enhances form based SQLInjection and Shell Injection.

# Who are we?
We are students of MESW (Software Engineering Masters) at FEUP (Porto Engineering University).

This was developed for Software Validation, Verification & Testing lecture as our State of the Art final project.

As we had to do a presentation about Security Testing we decided it would be great to improve ZAP and cover some failures we've encountered, during our testing for presentation.

# What do we think about security testing
Living without access to information at any time, from anywhere, through multiple devices is, nowadays, becoming unimaginable. Despite, information security is, now, more important than the access to that information.   
Lately, with the emerging of personal computers, smart phones, there are a lot of applications for everything, starting from searching on internet, to social networking, shopping, banking and a lot of more online services.

One can now imagine that there is a lot of information saved in our devices, such as, photos, documents, emails, conversations, important numbers, and lots of other type of information.
This information, critical or not, has to maintain its confidentiality. How can one guarantee it without testing? Well, he can't.

At first glance, one could think manual testing would suffice, but, what if the application scales, we have to test manually a lot of things and repeat the tests a million times or, even worse, we forget to test something that is really important.
This is when automate security testing arise. 

Automating security tests gives one the chance to just click a button to run a set of tests, saving a lot of time and effort at medium-long term, allows one to not forget about testing some feature and, probably more relevant, leads people to work together on producing scanning rules.

Although, keep in mind, this does not prevent, at all, zero day attacks. Still, what can prevent this type of attacks? Probably nothing. 

Summing up, automating security testing gives one the chance to test their application for known attacks in order to try to prevent them from happening.

Our opinion is that this subject is becoming more and more popular as technology evolves leading to a demand of increased security at twice the pace. Hence, we believe one should invest in this kind of tests, whether as usage or improvement, as we did on enhancing an extension for ZAP. 

![](https://github.com/pedroo21/ZAP-Multi-Scan-Rules/blob/master/imgs/security.jpg?raw=true)

# What about ZAP

### ZAP

ZAP is developed by OWASP (Open Web Application Security Project). It is one of the most popular free and actively maintained, by many volunteers, Security Testing Tools.    

It's meant to find security breaches in web applications while they're being developed and tested.

If you want to know more please visit their [website](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project)

### ZAP-Extensions
Because ZAP is open source it implies there's a community around it that is eager to improve the tool, as we did. In order to separate concerns and projects they decided to create an extensions repository, which is called [ZAP-Extensions](https://github.com/zaproxy/zap-extensions).
Here, you can develop your features and improvements, so they can be used, later, on ZAP.

# What did we find when we started developing
ZAP is not a small tool, thus meaning it's code is also not small.
As we started diving into code we find that there's two main scan rules, ascanrules which stands for active scanning rules and pscanrules standing for passive scanning rules.
We also discovered a lot more, but for starters purpose we're defining just the basic things.

### ASCANRULES
Active scanning rules is accounted for dealing with tests that do something in runtime, meaning they're actively "injecting" something, like Cross-Site Scripting (XSS), SQL Injection, Carriage Return Line Feed (CRLF), Path Traversal, Remote file include, and so on.

### PSCANRULES
Passive scanning rules refers to a set of rules that test for bad configurations, such as, Password Autocomplete, missing ContentType, X-XSS-Protection Header, etc.

### QUICKSTART
This package is, just as the name says, for starting with relative ease. We recommend you to use this, since it will save you a lot of time.   
Enables you to enter the website for testing, and executes all scans available.

![](https://github.com/pedroo21/ZAP-Multi-Scan-Rules/blob/master/imgs/quickstart.png?raw=true)

# Getting started
In this section we're going to explain what we did to start develop an extension for ZAP, so you can have an idea of what you need to do.    

1. Download/Clone/Fork ZAP github source code [here](https://github.com/zaproxy/zaproxy)
2. Download/Clone/Fork ZAP-Extensions github source code [here](https://github.com/zaproxy/zap-extensions)
3. We used IntelliJ and we had to do a few configurations. We describe them below
4. As ZAP-Extensions project is not runnable and it's using Ant as a build framework you need to open Ant Build window. In IntelliJ simply click on `View > Tool Windows > Ant Build`.
A window should appear looking like [this](https://github.com/pedroo21/ZAP-Multi-Scan-Rules/blob/master/imgs/ant.png?raw=true)
5. We recommend you to run `compile` on Ant window
6. Then, for starters, we ran `deploy-quickstart`. After it's completion in returns a .zap extension file that, if you have the both projects in the same directory, will automatically place itself in ZAP addons folder. Otherwise you'll have to move the file to `zaproxy/src/plugin`
7. Run ZAP. If everything went successful you should see a window like the one below.
![](https://github.com/pedroo21/ZAP-Multi-Scan-Rules/blob/master/imgs/zap.png?raw=true)
8. Congratulations! Quickstart is now deployed and working. If you enter a website nothing will be scanned, since ascanrules are not deployed yet. Though you can type a website, click `Attack` and see what happens for yourself
9. Now we're ready to deploy some ascanrules. Let's start by the easier ones. Open `ZapAddOn.xml` inside `ascanrules folder`.    
![](https://github.com/pedroo21/ZAP-Multi-Scan-Rules/blob/master/imgs/zapaddon.png?raw=true)
10. Comment line codes out like the image below
![](https://github.com/pedroo21/ZAP-Multi-Scan-Rules/blob/master/imgs/zapaddoncmt.png?raw=true)
11. Select `deploy-ascanrules` on Ant window and click `Run`
12. After its completion, re-run ZAP.
13. Retry the same test when you ran ZAP for the first time. If you spot any differences your application is vulnerable to XSS otherwise congratulations you're safe for XSS
15. If you want to add more rules to ZAP, just uncomment the lines you commented at step 10 and repeat the 11 to 13 steps. 
 
This was an easy introduction to what you have to do to build ZAP extensions or rules.

# IntelliJ Configuration
1. Open ZAP project.
2. Right click root folder and open module settings (Command + down arrow on MacOS)
3. In project if project compiler output is not set, set it to `"projectPath"/zaproxy/out`
4. Still in module settings go to modules tab select `zaproxy` and go to `paths` tab
5. In compiler output tick second option and set the `Output Path` to `"projectPath"/zaproxy/bin` and tick `Exclude output paths`
6. Move on to `Artifacts`
7. Click the `+` button and add a `Jar` from `Modules with Dependencies`
8. In the popup select the main class to be `ZAP` and click `Ok`
9. Change the name to `zap_dev:jar`
10. Set the output directory to `"projectPath"/zaproxy/build`
11. Tick `Build on Make`
12. Open `Run -> Edit Configurations` in IntelliJ
13. Add an `Application`
14. Name it `ZAP`. Set the `main class` to `org.zaproxy.zap.ZAP`
15. Set working directory to `"zaproxyPath"/build`
16. Set `use classpath of module` to `zaproxy`
17. If `before launch` is not set, click `+` and select `Make``
18. Click `Apply` and `Ok`
19. You're all set

# Developing an extension
We started by the basics, which were, for us, looking at other people's implementation. There was a pattern, and all of them extended AppPlugin, either via AbstractAppPlugin or AbstractAppParamPlugin.

After that we conclued that the ID for each extension had to be different. Also after implement all interface mandatory methods you must init the extension by calling `init()`. We did that in `scan()` method like `this.init(httpMessage, this.getParent())`

There's also another important function that is `bingo()`. Basically bingo allows us to generate an alert when a vulnerability is found. You must pass some arguments. Please check them `@bingo implementation`.

# Our extension
As we were testing ZAP for a presentation we developed an insecure website. We ran ZAP tests against it but we found that there was not scans for html input boxes, only for url queries.
So, we thought, there could be a real use for testing html requests within input boxes and that's why we started developing an extension to do that.

## How did we do it?
We used another tool, [Selenium](http://www.seleniumhq.org/), and integrated it with ZAP.

Selenium allows us to query for html elements, insert data and click into them.

### Form Based SQLInjection
Based on well known SQL strings and queries we try to inject code into the application, hoping it will lead us to use the system without the alleged authorization.

[![IMAGE ALT TEXT](http://img.youtube.com/vi/X1rsoT4a09Q/0.jpg)](http://www.youtube.com/watch?v=X1rsoT4a09Q "Video Title")

### Form Based Shell Injection
Based on Html File Input Type Element we try to upload a PHP Shell expecting to access the file system without authorization.

DISCLAIMER!   
Only Works in Chrome

1. Clone our github project [here](https://github.com/pedroo21/ZAP-Multi-Scan-Rules) into `ascanrules` at ZAP-Extensions
2. Open `JSONUtils` and change `jsonTxt` path to your ZAP-Extension directory and add `src/org/zaproxy/zap/extension/ascanrules/configs.json` to the end of it.
3. Change the `configs.json` to suit your needs
4. ShellDir -> File path to the shell to inject
5. SelectBtn -> Name of the HTML file selection button
6. SubmitBtn -> Name of the HTML submit button
7. UploadInject -> String of successful injection
8. PassField -> Password field name
9. Pass -> Shell Password
10. SuccShell -> Shell id to compare with DOM. If it matches shell was accessed
11. xPath -> Check an "a" element in DOM containing the link to the shell (if it was uploaded successfully)
12. SeleniumDriver -> File path to the selenium driver. If you don't have download it [here](https://sites.google.com/a/chromium.org/chromedriver/downloads)
13. Open Ant window and build `ascanrules`
14. Execute ZAP and test our extension




