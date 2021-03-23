# User Workflow

Visible design is a large part of the user experience, but so is the user's workflow, or how they interact with an app. In this section, we cover a few important steps of a typical workflow:

* **First-Launch Experience**: What the user sees the first time they use your app.
* **Normal Launch**: What happens when opening your app on a day-to-day basis.
* **Closing**: What happens when closing your app.
* **Background Tasks**: How your app manages to do things invisibly in the background.

## First-Launch Experience <a id="first-launch-experience"></a>

### Required Configuration <a id="required-configuration"></a>

When a user first launches an app, they should be able to get down to business as quickly as possible. If configuration is not absolutely required for the first use, they should not be required to configure anything. If configuration is required, they should be presented with a clean and simple [welcome screen](./#welcome-screen) within the app. Avoid separate configuration dialogs when launching.

### Speed of Launch <a id="speed-of-launch"></a>

Your app's first launch is the user's first impression of your app; it's a chance to really show off its design and speed. If your app has to configure things in the background before visibly launching, it gives the user the impression that the app is slow or will take a long time to start up. Instead, focus on making the application window appear fast and ready to be used, then do any background tasks behind the scenes. If the background task is blocking \(e.g. the user is unable to perform certain tasks until it's complete\), show some type of indication that a background process is happening and make the blocked user interface items insensitive \(see: [Widget Concepts](./#widget-concepts)\).

### Welcoming the User <a id="welcoming-the-user"></a>

If there is no content to show the user, provide actions they can act upon by using a simple [welcome screen](./#welcome-screen). Let them open a document, add an account, import a CD, or whatever makes sense in the context of the app.

### Resetting the App <a id="resetting-the-app"></a>

If a user explicitly "resets" the app \(ex. by deleting all songs in a music library or removing all mail accounts in a mail client\), it should return to its first-launch state.

## Normal Launch <a id="normal-launch"></a>

When a user launches an app, they're performing an explicit action and expecting a fast, oftentimes immediate response. You should focus on three key areas for app launching: speed, obviousness of what to do next, and state.

### Speed <a id="speed"></a>

As has been said before, speed, especially when launching an app, is very important. There should be as little delay as possible in between the time a user decides to launch an app and the instant they can begin using it. If your app requires a splash screen, you're doing it wrong.

### Obviousness <a id="obviousness"></a>

When a user launches your app, they should know exactly what to do next. This is achieved by following the other interface guidelines \(ensuring your app is consistent with other apps\) and by offering up explicit actions from the get go. If the app typically displays "items," such as songs or emails, let the user get at those items by displaying them when the app opens. If there are no previously-opened items, you should offer to open or create a new item \(such as a document\) by using a [welcome screen](./#welcome-screen).

### State <a id="state"></a>

If the user has previously used your app, it's typically best to restore the state of the app when opening it again. This means the app comes up to right where the user left off so they can pick up their work again. For a music player, this means opening up with the view where the user left it and the song paused where the user closed the app. For a document editor, this would mean opening up with the same document scrolled to the same spot with the cursor in the same spot on the page.

## Always Provide an Undo <a id="always-provide-an-undo"></a>

Sometimes a user will perform an action which could possibly be destructive or traditionally irreversible. Rather than present the user with a warning, apps should let the user undo the action for an appropriate amount of time. Some prime examples of when this behavior is useful are:

* **Closing an app**. Rather than warning the user, automatically save their work and the app's state so they can return exactly where they left off. See [Closing](./#closing).
* **Deleting an item**. Instead of asking the user if they are sure, make the item "disappear" from the app, but provide an easy and intuitive way to undo the delete.
* **Sending an email**. Rather than asking the user if they want to send an email, let them undo or edit the message a short time after "sending."
* **Editing a photo**. Instead of asking the user if they want to destructively apply an edit, let them undo the edit and always keep the original backed up.

This behavior should only as a last resort be implemented by providing a buffer time between when the app shows the user what happened and actually performing the action. To keep the experience responsive, the app should always look as if it performed the action as soon as the user initiates it.

This behavior strikes the best balance of keeping out of the user's way while making sure they don't do something unintended. It's important to keep the undo action unobtrusive yet simple and intuitive; a common way of doing so is by using an info bar, though other methods may also be appropriate.

See also: [Never Use a Warning When you Mean Undo](https://alistapart.com/article/neveruseawarning) by Aza Raskin

## Always Saved <a id="always-saved"></a>

Users should feel confident when using elementary OS; they should know that everything they see is saved and up to date.

Apps in elementary OS should operate around an always-saved state. This means that changes the user makes are instantly applied and visible and that making the user manually save things is a legacy or specialized behavior.

For example, a Song Info dialog should update the track information instantly without a user having to press a save button, user preferences should be applied as soon as the user manipulates the relevant widget, and closing an app should mean that reopening it will return to where the user left off.

## Closing <a id="closing"></a>

When a user closes an app, it's typically because they're done using it for now and they want to get it out of the way.

### Saving State <a id="saving-state"></a>

Apps should save their current state when closed so they can be reopened right to where the user left off. Typically, closing and reopening an app should be indistinguishable from the legacy concept of minimizing and unminimizing an app; that is, all elements should be saved including open documents, scroll position, undo history, etc.

Because of the strong convention of saved state, elementary OS does not expose or optimize for legacy minimize behavior; e.g. there is no minimize button, and the Multitasking View does not distinguish minimized windows.

### Closing the App Window <a id="closing-the-app-window"></a>

Apps should never minimize instead of closing, as that puts the app window into a state that is foreign to users of elementary OS. Instead, windows should close or hide and re-open with a [saved state](./#saving-state). Any ongoing or [background tasks](./#background-tasks) should be completed soon after the window is closed, then the app should quit so as to not use unnecessary resources.

