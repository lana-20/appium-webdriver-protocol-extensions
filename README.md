# Appium's Protocol Extensions

*Appium exposes a WebDriver API just like Selenium. But we can do more with mobile devices than we can with web browsers. So how does Appium provide access to these features that would never be part of a web-based automation API?*

The WebDriver Protocol was developed by the Selenium project team in conjunction with the W3C standards group, and members of the various companies that produce the web browsers we all use, like Google, Apple, Mozilla, and so on. Their whole purpose was to come up with an automation API for web browsers and web applications. They obviously were aware of non-web apps, like mobile device apps, but their focus was not on building an automation API for anything other than web browsers. What this means is that, as you look at the list of commands available in the WebDriver API, you'll find only commands that are relevant for testing websites.

But what about mobile apps? Is the WebDriver Protocol sufficient for everything we want to do for automating mobile apps? Well, it certainly gets us a lot of the way there. Much of the WebDriver Protocol isn't limited conceptually to websites. Both websites and mobile apps have user interfaces that are based around interacting with elements. But some parts of the WebDriver Protocol really only make sense when it comes to websites. Getting the URL of the current page, for example, is not an action that makes any sense when using the Weather app on your phone. Likewise, mobile apps rely on various technologies that don't exist in web browsers at all. For example, you can control some mobile apps by turning the device in various directions, relying on an internal accelerometer to give the app information about the device's state. Or, more boringly perhaps, devices usually have some kind of home button or action used to return to the home screen. Mobile devices are their own little computers with their own filesystem, whereas web browsers are not. The differences can become quite significant.

So there are two questions for a project like Appium, that wants to use the WebDriver Protocol to implement automation for mobile devices. The first is, what to do with the commands that don't make sense on mobile. And the second is, how to implement support for commands that would be really useful for mobile, but don't exist in the WebDriver protocol.

The answer to the first question is pretty easy. If there's something that doesn't make sense for mobile, Appium could just choose not to implement it! And this is what Appium does, although in fact Appium also provides support for mobile web browsers, so Appium ends up supporting the entire WebDriver Protocol as it is anyway. The answer to the second question, about how to provide support for mobile-specific behaviors, is a bit tougher.

Ultimately, Appium wants to make sure that you have the automation capabilities you need, even if they go beyond the WebDriver Protocol's boundaries. And the way we provide that support is by extending the WebDriver Protocol. We add support for new commands not by breaking the protocol, but merely by extending it. The Protocol as it stands for the web is basically a big list of routes and rules about what sorts of parameters those routes expect and what sorts of responses they will generate. All Appium does is add a bunch more routes to that list!

What this means is that if you want to know all the commands that Appium supports, you can't just go looking at the WebDriver Protocol documentation. Because Appium has added a bunch of its own extensions, which would only be found in the Appium documentation. You can think of Appium's protocol like a superset of the WebDriver protocol. And this is in fact how the WebDriver Protocol was defined. The authors knew that other projects might want to extend it with their own commands, so it provides rules for how to do that in a way which is approved by the standard. And that's what the Appium team did!

Let's briefly look at a few examples.

    POST /session/{session id}/appium/device/lock
    POST /session/{session id}/appium/device/unlock
    POST /session/{session id}/appium/device/app_installed

These three examples represent the ability to lock a device's screen, unlock the screen, and check whether an app is installed on the device. None of these would make sense in the context of a web browser, so Appium added the commands as extensions to the protocol. Notice that for each of the routes, they all have a <code>/appium</code> in the middle. This is to make sure that Appium's command extensions will never clash with official extensions to the protocol.

Otherwise, the Appium extensions work exactly the same way from a protocol perspective as their standard counterparts. They take the same types of parameters and respond with the same types of values or error messages.

All this to say, it's good to be aware that Appium has extended the WebDriver protocol in a standard-compliant way, to provide additional features specifically for the purpose of automating mobile apps.


