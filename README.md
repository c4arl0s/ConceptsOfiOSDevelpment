# ConceptsOfiOSDevelpment
Concepts of iOS Development splited in txt files.
Add this line from master
This branch is created to add more concepts of iOS Development

<p align="center">
    <img src="https://github.com/carlos-santiago-2017/ConceptsOfiOSDevelpment/blob/master/screenshoot.png" width="675">
</p>

comment: A piece of text in a source code file that doesn't get compiled as part of the program but provides context or other useful information about individual pieces of code.
Conflicting Constraints: Too many constraints. For example a button, cannot be in two places at the same time.

console: A tool for debugging and for logging information for debugging purposes.

constant: A value that's initialized once and cannot change, indicated in Swift by the let keyword.

constraint: In Auto Layout, a rule that explains where one element should be located relative to another, what size it should be, or which of two elements should shrink first when something reduces the space available for each of them.

Constraints: It is the relations between views. Basically, there are two types of constraints for a view. One is the size an space betwwn views. usually neighbor views. These we call pins. The other is between two specific views by an attribute of the view. These we call alighment or aligns.

Constraint Error: Once you start working with constraints, you will get a lot of warnings. All errors for constraints start as a warning, though they may become fatal errors at runtime. You will need to resolve all these errors. There are three types of errors: misplaced views, missing constraints and conflicting constraints.content view: A view object that's located at the top of a view hierarchy, serving as a container for the subviews in its hierarchy.

control: A specialized type of view (specifically, an instance of the UIControl class or one of its subclasses) that responds to user input.
convenience initializer: A secondary initializer, which adds additional behavior or customization, but must eventually call through to a designated initializer.

Core Motion: Process accelerometer, gyroscope, pedometer, and environment-related events.Databases are used for large quantities of data. They use:

* Tables, which store data.
* Schemas, which define the kind of information stored in a Table.
* Queries, which are used to retrieve or manipulate data from tables.
* Views, which hold results of queries.data model: The representation or structure of data within an app.

data source: An object that manages the app's data model, providing a view object with the information it needs to display that data.

delegate: An object that acts on behalf of, or in coordination with, another object.

Delegation is used for everything from handling table view events using UITableViewDelegate, to modifying cache behavior using NSCacheDelegate. The core purpose of the delegate pattern is to allow an object to communicate back to its owner in a decoupled way.

When to delegate ?

Delegation is usually a good choice when a type needs to be usable in many different contexts.

Definition
Adventages:	Reusabilidad, loose Coupling, Separation of Responsabilities.

designated initializer: One of the primary initializers for a class; a convenience initializer within a class must ultimately call through to a designated initializer.

destination view controller: The view controller whose contents are displayed at the end of a segue.

downcast: To attempt to cast an object to one of its subclass types.

entry point: Where control enters a program or piece of code.

enumeration: A data type that defines a group of related values and enables you to work with those values in a type-safe way within your code. Enumerations are a convenient way of defining and restricting the possible values of a variable. Associated values are a useful feature of enumerations. 

Enumerations and Associated Values: Associated values are a useful feature of enumerations. Let’s take a moment to look at a simple example before you use this feature in Photorama.

Enumerations are a convenient way of defining and restricting the possible values for a variable. 

For example, let’s say you are working on a home automation app. You could define an enumeration to specify the oven state, like this:

enum OvenState {
  case on
	case off 
}

enum OvenState {
	case on(Double)
	case off 
}
var ovenState = OvenState.on(450)

Each case of an enumeration can have data of any type associated with it. 

For OvenState, its .on case has an associated Double that represents the oven’s temperature. Notice that not all cases need to have associated values.

Retrieving the associated value from an enum is often done using a switch statement.

switch ovenState {
	case let .on(temperature):
			print("The oven is on and set to \(temperature) degrees.")
	case .off: 
			print("The oven is off.")
}

Note that the .on case uses a let keyword to store the associated value in the temperature constant, which can be used within the case clause. (You can use the var keyword instead if temperature needs to be a variable.)

Considering the value given to ovenState, the switch statement above would result in the line The oven is on and set to 450 degrees. printed to the console.event-driven programming: A category of programming in which the flow of the app is determined by events: system events and user actions.

extension: A capability to add functionality to an existing type.
failable initializer: An initializer that could return nil after initialization.
Receive data directly into memory by creating a data task from a URL session.

Overview
For small interactions with remote servers, you can use the URLSessionDataTask class to receive response data into memory (as opposed to using the URLSessionDownloadTask class, which stores the data directly to the file system). A data task is ideal for uses like calling a web service endpoint.

You use a URL session instance to create the task. If your needs are fairly simple, you can use the shared instance of the URLSession class.

If you want to interact with the transfer through delegate callbacks, you’ll need to create a session instead of using the shared instance. 

 You use a URLSessionConfiguration instance when creating a session, also passing in a class that implements URLSessionDelegate or one of its subprotocols. 

Sessions can be reused to create multiple tasks, so for each unique configuration you need, create a session and store it as a property.

Note: Be careful to not create more sessions than you need. For example, if you have several parts of your app that need a similarly configured session, create one session and share it among them.

Once you have a session, you create a data task with one of the dataTask() methods. Tasks are created in a suspended state, and can be started by calling resume().

Receive Results with a Completion Handler

- The simplest way to fetch data is to create a data task that uses a completion handler. 
- With this arrangement, the task delivers the server’s response, data, and possibly errors to a completion handler block that you provide. 
- Please see the picture. It shows the relationship between a session and a task, and how results are delivered to the completion handler.

+------------+----------------+--------------------+---------------------------------------------+-------------------+
| URLSession | -- creates --> | URLSessionDataTask | -- send (data, request, error) parameters.--> | CompletionHandler |
+------------+----------------+--------------------+---------------------------------------------+-------------------+

- To create a data task that uses a completion handler, call the dataTask(with:) method of URLSession. Your completion handler needs to do three things:

1.- Verify that the error parameter is nil. If not, a transport error has occurred; handle the error and exit.
2.- Check the response parameter to verify that the status code indicates success and that the MIME type is an expected value. If not, handle the server error and exit.
3.- Use the data instance as needed.

Listing 1 shows a startLoad() method for fetching a URL’s contents. 
- It starts by using the URLSession class’s shared instance to create a data task that delivers its results to a completion handler. 
- After checking for local and server errors, this handler converts the data to a string, and uses it to populate a WKWebView outlet. 
- Of course, your app might have other uses for fetched data, like parsing it into a data model.

Listing 1 
Creating a completion handler to receive data-loading results

func startLoad() {
    let url = URL(string: "https://www.example.com/")!
    let task = URLSession.shared.dataTask(with: url) { data, response, error in
        if let error = error {
            self.handleClientError(error)
            return
        }
        guard let httpResponse = response as? HTTPURLResponse, (200...299).contains(httpResponse.statusCode) else { 
						self.handleServerError(response)
            return
        }
        if let mimeType = httpResponse.mimeType, mimeType == "text/html",
            let data = data,
            let string = String(data: data, encoding: .utf8) {
            DispatchQueue.main.async {
                self.webView.loadHTMLString(string, baseURL: url)
            }
        }
    }
    task.resume()
}



first responder: An object that is first to receive many kinds of app events, including key events, motion events, and action messages, among others.

fix-it: A suggested fix for a compiler error in Xcode.

force-unwrap operator: An operator (!) placed after an optional value to access its underlying value.

forced type cast operator: An operator (as!) that attempts a downcast and force-unwraps the result.

function: A reusable, named piece of code that can be referred to from many places in a program.

Functions menu: In Xcode, a jump menu that lets you navigate directly to a specific declaration or section in a source code file.

gesture recognizer: An object that you attach to a view that allows the view to respond to actions the way a control does.

global: A constant, variable, or function defined at the top-level scope of a program.

it is a variable that can be accessed from any function at any time. We call these global variables. To make a variable global, you declare it outside of a particular function. action:	A piece of code that's linked to an event that can occur in your app.

activity viewer:	Part of the Xcode toolbar that displays messages about the build process and other information.

adaptive interface: A user interface (UI) that automatically adjusts so that it looks good in the context of the available screen space.

adopt: To indicate that a class, structure, or enumeration conforms to a protocol.

application programming interface (API): A set of functions, classes, protocols, and other components that define how pieces of software should interact with each other.

app delegate: An object in your app (specifically, an instance of the AppDelegate class) that creates the window where your app's content is drawn and that provides a place to respond to state transitions within the app.

application object: An object in your app that's responsible for managing the life cycle of the app, communicating with its delegate, the app delegate, during state transitions within the app.

argument: A value you pass in to a function, method, or initializer to satisfy one of its parameters.

array: A data type that stores multiple values of the same type in an ordered list.

Attributes inspector: An inspector that you use to customize visual attributes of a user interface (UI) element in a storyboard.

asset catalog: A tool to manage assets like images that are used by your app as part of its user interface (UI).

assistant editor: In Xcode, a secondary editor window that appears side-by-side with your primary editor.

Auto Layout: A layout engine that helps lay out your user interface (UI) based on the constraints you specify.

base class: A class that's at the root of its class hierarchy, meaning that it has no superclass.

canvas: The background of a storyboard where you add and arrange user interface (UI) elements.

class: A piece of code that describes the behavior and properties common to any particular type of object, essentially providing a blueprint for the object.

clean: Removes all the product files, as well as any object files or other intermediate files created during the build process.

class hierarchy: A hierarchical representation of a class's relationships to its superclass and subclasses.

closed range operator: An operator (...) that lets you create a range of numbers that includes both the lower and upper values.

closure: A self-contained block of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and to lambdas in other programming languages.

Cocoa Touch: The set of Apple frameworks and technologies used to develop iOS apps.

code completion: A feature of Xcode that infers what you're trying to type from context and provides suggestions that you can select.

completion handler: A closure that's passed as a parameter to a method that calls the closure when it finishes executing.

comment: A piece of text in a source code file that doesn't get compiled as part of the program but provides context or other useful information about individual pieces of code.

conditional statement: A control flow statement that checks whether a condition is true before executing a piece of code.

conform to: For a class, structure, or enumeration to satisfy the requirements of a protocol.

console: A tool for debugging and for logging information for debugging purposes.

constant: A value that's initialized once and cannot change, indicated in Swift by the let keyword.

constraint: In Auto Layout, a rule that explains where one element should be located relative to another, what size it should be, or which of two elements should shrink first when something reduces the space available for each of them.

content view: A view object that's located at the top of a view hierarchy, serving as a container for the subviews in its hierarchy.

control: A specialized type of view (specifically, an instance of the UIControl class or one of its subclasses) that responds to user input.

convenience initializer: A secondary initializer, which adds additional behavior or customization, but must eventually call through to a designated initializer.

data model: The representation or structure of data within an app.

data source: An object that manages the app's data model, providing a view object with the information it needs to display that data.

delegate: An object that acts on behalf of, or in coordination with, another object.

designated initializer: One of the primary initializers for a class; a convenience initializer within a class must ultimately call through to a designated initializer.

destination view controller: The view controller whose contents are displayed at the end of a segue.

downcast: To attempt to cast an object to one of its subclass types.

entry point: Where control enters a program or piece of code.

enumeration: A data type that defines a group of related values and enables you to work with those values in a type-safe way within your code.

event-driven programming: A category of programming in which the flow of the app is determined by events: system events and user actions.

extension: A capability to add functionality to an existing type.

failable initializer: An initializer that could return nil after initialization.

first responder: An object that is first to receive many kinds of app events, including key events, motion events, and action messages, among others.

fix-it: A suggested fix for a compiler error in Xcode.

forced type cast operator: An operator (as!) that attempts a downcast and force-unwraps the result.

force-unwrap operator: An operator (!) placed after an optional value to access its underlying value.

function: A reusable, named piece of code that can be referred to from many places in a program.

Functions menu: In Xcode, a jump menu that lets you navigate directly to a specific declaration or section in a source code file.

gesture recognizer: An object that you attach to a view that allows the view to respond to actions the way a control does.

global: A constant, variable, or function defined at the top-level scope of a program.

guard: A guard statement declares a condition that must be true in order for the code after the guard statement to be executed. Using a guard statement for requirements improves the readability of your code, compared to doing the same check with an if statement.

half-open range operator: An operator (..<) that lets you create a range of numbers that includes the lower but not the upper value.

Identity inspector: An inspector that you use to edit properties of an object in a storyboard related to that object's identity, such as what class the object belongs to.

identity operator: An operator (===) that tests whether two object references both refer to the same object instance.

immutable: A value that cannot be changed (or mutated) after it's initialized, like a constant.

implement: To define the behavior of something in code.

implicitly unwrapped optional: An optional that can also be used like a nonoptional value, without the need to unwrap the optional value each time it is accessed, because it's assumed to always have a value after that value is initially set.

inheritance: When a class is a subclass of another class, it gets all of its behavior (methods, properties, and other characteristics) from its superclass.

initializer: A method that handles the process of preparing an instance of a class, structure, or enumeration for use, which involves setting an initial value for its properties and performing any other required setup.

inspector pane: An area in Xcode that displays inspectors, such as the Attributes inspector, Identity inspector, and Size inspector.

instance: A specific occurrence of a class (that is, an object), structure, or enumeration.

integrated development environment (IDE): A software application that provides a set of tools for software development.

Interface Builder: The graphical environment for building a user interface (UI) in Xcode.

intrinsic content size: The minimum size needed to display all the content in a view without clipping or distorting that content.

iterate: To perform repeatedly.

library pane: An area in Xcode that displays one of the ready-to-use libraries of resources for your project, like the Object library.

local: A constant or variable defined only within a particular, limited scope, like a loop, conditional statement, or function.

loop: A control flow statement that executes the same piece of code multiple times.

method: A reusable, named piece of code that's associated with a particular class, structure, or enumeration.

modal segue: A segue in which one view controller presents another view controller as its child. The user must interact with the presented controller, and dismiss it before returning to the app's main flow. Use modal segues to present tasks that the user must complete before continuing.

Model-View-Controller: (MVC) A pattern of app design in which view controllers serve as the communication pipeline between views and the data model.

mutable: A value that is able to be changed (or mutated) after it's initialized, like a variable.

navigation controller: A specialized view controller subclass that manages transitions backward and forward through a series of view controllers.

navigation stack: The set of view controllers managed by a particular navigation controller.

nil: The absence of a value or no value.

nil coalescing operator: An operator (??) placed between two values, a ?? b, that unwraps an optional a if it contains a value, or returns a default value b if a is nil.

object: An instance of a class.

Object library: Part of the Xcode workspace window that shows a list of objects that can be added to a storyboard, including each object's name, description, and visual representation.

optional: A value that contains either an underlying value or nil to indicate that the value is missing.

optional binding: The process of attempting to assign an optional value to a constant in a conditional statement to see if the optional contains an underlying value.

optional type cast operator: An operator (as?) that attempts a downcast and returns the result as an optional value.

outlet: A reference to an object in a storyboard from a source code file.

outline view: A pane in a storyboard that lets you see a hierarchical representation of the objects in your storyboard.

override: To replace an implementation of a method defined on a superclass.

parameter: An additional piece of information that must be passed into a function, method, or initializer when it's called.

playground: A type of file in which you can change and play around with Swift code directly in Xcode and see the immediate results.

project navigator: Part of the Xcode workspace window that displays all the files in your project.

property: A piece of data encapsulated within a class, structure, or enumeration.

property observer: A piece of code that's called every time the value of a property is set. Use property observers to observe and respond to changes in the property's value.

protocol: A blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality.

read-only: A value that can only be viewed (read) but never changed (written).

read-write: A value that can be both viewed (read) and changed (written).

resize handles: Small white squares that appear on a user interface (UI) element's borders when it's selected so you can change its size on the canvas.

root view controller: The first item added to a the navigation stack of a navigation controller. The root view controller is never popped off (removed from) the stack.

run loop: An event processing loop that you use to schedule work and coordinate the receipt of incoming events in your app.

runtime: The period during which a program is executing.

scene: A storyboard representation of a screen of content in your app.

scene dock: A bar that contains information related to a scene in a storyboard.

segue: A transition from one scene to another in a storyboard.

show segue: A segue that varies the way new content is displayed based on the target view controller. For navigation controllers, the show segue pushes new content on top of the current view controller stack. Use a navigation controller and show segues to navigate through hierarchical data.

Simulator: An app in Xcode that simulates the behavior and appearance of running an app on a device.

Size inspector: An inspector that you use to edit the size and position of a user interface (UI) element in a storyboard.

source view controller: The view controller whose contents are displayed at the beginning of a segue.

storyboard: A file that contains a visual representation of the app's UI (user interface), showing screens of content and the transitions between them, that you work on in Interface Builder.

storyboard entry point: The first scene that's shown from a storyboard when an app starts.

string interpolation: The process of inserting string representations of constants, variables, literals, and expressions into longer strings.
structure: A data type that's similar to a class, but doesn't support inheritance and is passed by value instead of by reference.

subclass: A class that's a child of another class (known as its superclass).

subview: A view that is enclosed by another view (known as its superview).

superclass: A class that's a parent of another class (known as its subclass).

superview: A view that encloses another view (known as its subview).

Swift standard library: A set of data types and capabilities designed for Swift and baked into the language.

target: The object that receives the action message in the target-action pattern.

target-action: A design pattern in which one object sends a message to another object when a specific event occurs.

tuple: A grouping of values.

type casting: A way to check the type of an object, and to treat that object as if it's a different superclass or subclass from somewhere else in its own class hierarchy.

type inference: The ability of the Swift compiler to determine the type of a value from context, without an explicit type declaration.

UIKit: A Cocoa Touch framework for working with the user interface (UI) layer of an iOS app.

underscore: A representation of a wildcard in Swift (_).

unit test: A piece of code written specifically to test a small, self-contained piece of behavior in your app to make sure it behaves correctly.

unwrap: To extract an underlying value from an optional.

user interface (UI): The layer of visual elements that lets a user interact with a piece of software.

utility area: An area in Xcode that displays the inspector pane and .

unwind segue: A type of segue used to implement backward navigation.

variable: A value that can change after it's been initialized, indicated in Swift by the var keyword.

view: An object that's used to construct your user interface (UI) and display content to the user.

view controller: An object that manages a set of views and coordinates the flow of information between the app's data model and the views that display that data.

view hierarchy: A hierarchical representation of views relative to other views.

workspace window: The Xcode window, which you use to manage and navigate through the files and resources in your project.

guard: A guard statement declares a condition that must be true in order for the code after the guard statement to be executed. Using a guard statement for requirements improves the readability of your code, compared to doing the same check with an if statement.

half-open range operator: An operator (..<) that lets you create a range of numbers that includes the lower but not the upper value.

Identity inspector: An inspector that you use to edit properties of an object in a storyboard related to that object's identity, such as what class the object belongs to.

identity operator: An operator (===) that tests whether two object references both refer to the same object instance.

immutable: A value that cannot be changed (or mutated) after it's initialized, like a constant.

implement: To define the behavior of something in code.

implicitly unwrapped optional: An optional that can also be used like a nonoptional value, without the need to unwrap the optional value each time it is accessed, because it's assumed to always have a value after that value is initially set.

inheritance: When a class is a subclass of another class, it gets all of its behavior (methods, properties, and other characteristics) from its superclass.

initializer: A method that handles the process of preparing an instance of a class, structure, or enumeration for use, which involves setting an initial value for its properties and performing any other required setup.

inspector pane: An area in Xcode that displays inspectors, such as the Attributes inspector, Identity inspector, and Size inspector.

instance: A specific occurrence of a class (that is, an object), structure, or enumeration.

integrated development environment (IDE): A software application that provides a set of tools for software development.

Let’s look at some methods that are called during the lifecycle of a view controller and its view. Some of these methods you have already seen, and some are new.


init(coder:) is the initializer for UIViewController instances created from a storyboard. When a view controller instance is created from a storyboard, its init(coder:) gets called once. You will learn more about this method in Chapter 16.

init(nibName:bundle:) is the designated initializer for UIViewController.

When a view controller instance is created without the use of a storyboard, its init(nibName:bundle:) gets called once. Note that in some apps, you may end up creating several instances of the same view controller class. This method will get called once on each view controller as it is created.

loadView() is overridden to create a view controller’s view programmatically.

viewDidLoad() is overridden to configure views created by loading an interface file. This method gets called
after the view of a view controller is created.

viewWillAppear(_:) is overridden to configure views created by loading an interface file.

This method and viewDidAppear(_:) get called every time your view controller is moved onscreen. viewWillDisappear(_:) and viewDidDisappear(_:) get called every time your view controller is moved offscreen.Interface Builder: The graphical environment for building a user interface (UI) in Xcode.

intrinsic content size: The minimum size needed to display all the content in a view without clipping or distorting that content.

iterate: To perform repeatedly.

JSONSerialization: The JSONSerialization class is responsible for returning a Data object, which can then be passed as an HTTPBody to a request.

Any number of things could go wrong, such as:

* the JSON is just completely invalid (missing an opening brace, a closing brace, a comma, quotation marks, or something else)
* you expect an integer in the JSON but get a string (or you expect a boolean and get an integer, or whatever…)
* one of the values in the JSON is null
* the structure of the JSON is different from what you expec.

JSON, stands for JavaScript Object Notation

Data is a collection of symbols on which operations are performed usually by computers. Data is quantitative, it takes up storage such as 3 kilobytes. For example, a piece of data is “June 2, 2014”, a date.


library pane: An area in Xcode that displays one of the ready-to-use libraries of resources for your project, like the Object library.

local: A constant or variable defined only within a particular, limited scope, like a loop, conditional statement, or function.

loop: A control flow statement that executes the same piece of code multiple times.

method: A reusable, named piece of code that's associated with a particular class, structure, or enumeration.

Missin Constraints: a second kind of error is missing constraints, sometimes referred to as ambiguous constraints. All views using constraints need enough information to determine location and size of the view.modal segue: A segue in which one view controller presents another view controller as its child. The user must interact with the presented controller, and dismiss it before returning to the app's main flow. Use modal segues to present tasks that the user must complete before continuing.

Model-View-Controller: (MVC) A pattern of app design in which view controllers serve as the communication pipeline between views and the data model.

- Use AppDelegate method to handle different events in the app life cycle.
- Edit Main.storyboard file in Interface Builder to define views an create user interfaces.

MODEL
- A model object groups the data you need for a specific problem domain or a type of solution you are trying to build.
- Model objects can be related to other model objects.
- Most cases, you will create model objects by defining new structures or classes in your object.
- Typically define structures an classes in a new swift file.

Comminication
- Model objects are usualu created in response to some user interaction with the view or a control. 
- The message to create the model object is transmitted from the view through a controller object, which is most often a subclass of a viewcontroller.
- Model objects should not have any direct connection to views.

VIEWS
- A view object knows ho to draw itself on the screen and may respond to user input.
- View Objects display data about and apps model objects and to allow the user to edit that data.
- Views can be reused or reconfigured to show different instances of model data.
- Views often have an update or configure function that accepts a model object as a parameter, and uses the model object to update itself to match the data it is mean to display.

CONTROLLERS
- A controller object acts as the messenger between views and model objects.
Three reasons to create a controller
1.- Multiple objects or scenes need access to the model data.
2.- The logic for adding, modifying, or deleting model data is complex.
3.- You want to keep the code in your view controllers focused on magagin the views.

Helper COntrollers
- NetworkController
- NoteListViewController
- NoteDetailViewController

Communication

- COntroller objects are free to communicate or work directly with other objects.

mutable: A value that is able to be changed (or mutated) after it's initialized, like a variable.

The root class of most Objective-C class hierarchies, from which subclasses inherit a basic interface to the runtime system and the ability to behave as Objective-C objects.

navigation controller: A specialized view controller subclass that manages transitions backward and forward through a series of view controllers.

navigation stack: The set of view controllers managed by a particular navigation controller.

nil: The absence of a value or no value.

nil coalescing operator: An operator (??) placed between two values, a ?? b, that unwraps an optional a if it contains a value, or returns a default value b if a is nil.

object: An instance of a class.

Object library: Part of the Xcode workspace window that shows a list of objects that can be added to a storyboard, including each object's name, description, and visual representation.

optional: A value that contains either an underlying value or nil to indicate that the value is missing.

is the process of attemping to assign an optional value to a constant in a conditional statement to see if the optional contains an underlying value.

.optional binding: The process of attempting to assign an optional value to a constant in a conditional statement to see if the optional contains an underlying value.

optional type cast operator: An operator (as?) that attempts a downcast and returns the result as an optional value.

outlet: A reference to an object in a storyboard from a source code file.

outline view: A pane in a storyboard that lets you see a hierarchical representation of the objects in your storyboard.

override: To replace an implementation of a method defined on a superclass.

parameter: An additional piece of information that must be passed into a function, method, or initializer when it's called.

Pins: For a pin, you select one object and describe how far away it is from its nearest neightbors. All pins constraints are foun on the pin button. If you were to select a view and open the pin menu with the icon, you would see this: See the image.playground: A type of file in which you can change and play around with Swift code directly in Xcode and see the immediate results.

project navigator: Part of the Xcode workspace window that displays all the files in your project.

property: A piece of data encapsulated within a class, structure, or enumeration.

property observer: A piece of code that's called every time the value of a property is set. Use property observers to observe and respond to changes in the property's value.

protocol: A blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The most common way of delegation that is found in Apples own APIs is by using delegate protocols.

REST web Service: All I mean by "REST web service" or even when I say "web service" or "API" is that we can send an HTTP request and we get back some data in a format thats easy to use in our app. Usually that format will be JSON.

read-only: A value that can only be viewed (read) but never changed (written).

read-write: A value that can be both viewed (read) and changed (written).

resize handles: Small white squares that appear on a user interface (UI) element's borders when it's selected so you can change its size on the canvas.

root view controller: The first item added to a the navigation stack of a navigation controller. The root view controller is never popped off (removed from) the stack.

run loop: An event processing loop that you use to schedule work and coordinate the receipt of incoming events in your app.

runtime: The period during which a program is executing.

scene dock: A bar that contains information related to a scene in a storyboard.

SceneKit : A framework that combines a high-performance rendering engine with a descriptive API, allowing 3D content to be controlled and displayed.segue: A transition from one scene to another in a storyboard.

self: is a property on the instance that refers to itself. It's used to access class, structure and enumeration instance within methods.
struct Person {
    var name: String
    var age: Int
    
    // you can take advantage of your knowledge of variable shadowing to create clean, easy-to-read initializers.
    // Suppose you want to create an instance of a Person by passing in a name and age as its two parameters. You will also assume that every Person instance has both name and age properties.
    // As you are writing the initializer, you will want to keep it as simple and logical as possible: assigning the bane parameter to the name property ans assigning the age parameter to the age property.
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    // since name and age are the names of parameters within the function scope, they shadow the name and age properties defined within the Person scope.
    // you can place the keyword self in front of the property name to reference the property specifically- and to avoid any confusion that the variable shadowing may cause to the compiler and the reader. This syntax majes it very clear that the name and age properties are set to the name and age parameters passed into the initializer.
}
show segue: A segue that varies the way new content is displayed based on the target view controller. For navigation controllers, the show segue pushes new content on top of the current view controller stack. Use a navigation controller and show segues to navigate through hierarchical data.

Simulator: An app in Xcode that simulates the behavior and appearance of running an app on a device.

Size inspector: An inspector that you use to edit the size and position of a user interface (UI) element in a storyboard.

source view controller: The view controller whose contents are displayed at the beginning of a segue.

Any complex program will involve dozen of files containing different functions. Global variables are available to the code in every one of those files. Sometimes sharing a variable between different files is what you want. But as you can imagine, having a variable that can be accessed by multiple functions can also lead to great confusion.

A Static variable is like a global variable in that it is declare outside of any function. However, a static variable is only accessible from the code in the file where it was declared.

storyboard: A file that contains a visual representation of the app's UI (user interface), showing screens of content and the transitions between them, that you work on in Interface Builder.

storyboard entry point: The first scene that's shown from a storyboard when an app starts.

string interpolation: The process of inserting string representations of constants, variables, literals, and expressions into longer strings.

structure: A data type that's similar to a class, but doesn't support inheritance and is passed by value instead of by reference.

subclass: A class that's a child of another class (known as its superclass).

subview: A view that is enclosed by another view (known as its superview).

superclass: A class that's a parent of another class (known as its subclass).

superview: A view that encloses another view (known as its subview).

Swift standard library: A set of data types and capabilities designed for Swift and baked into the language.

target-action: A design pattern in which one object sends a message to another object when a specific event occurs.

target: The object that receives the action message in the target-action pattern.

# Glossary Programming in Objective-C - Stephen G. Kochan.

**automatic variable** : A variable that is automatically allocated and released when a statement block is entered and exited.Automatic variables have scope that is limited to the block in which they are defined and have no default initial value.They are optionally preceded by the keyword auto.

The entry point for every C-based app is the main function and iOS apps are no different. What is different is that for iOS apps you do not write the main function yourself. Instead, Xcode creates this function as part of your basic project. Listing 2-1 shows an example of this function. With few exceptions, you should never change the implementation of the main function that Xcode provides.

Listing 2-1  The main function of an iOS app
#import <UIKit/UIKit.h>
#import "AppDelegate.h"
 
int main(int argc, char * argv[])
{
    @autoreleasepool {
        return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
    }
}
The only thing to mention about the main function is that its job is to hand control off to the UIKit framework. The UIApplicationMain function handles this process by creating the core objects of your app, loading your app’s user interface from the available storyboard files, calling your custom code so that you have a chance to do some initial setup, and putting the app’s run loop in motion. The only pieces that you have to provide are the storyboard files and the custom initialization code.

An app’s main run loop processes all user-related events. The UIApplication object sets up the main run loop at launch time and uses it to process events and handle updates to view-based interfaces. As the name suggests, the main run loop executes on the app’s main thread. This behavior ensures that user-related events are processed serially in the order in which they were received.

Figure 2-2 shows the architecture of the main run loop and how user events result in actions taken by your app. As the user interacts with a device, events related to those interactions are generated by the system and delivered to the app via a special port set up by UIKit. Events are queued internally by the app and dispatched one-by-one to the main run loop for execution. The UIApplication object is the first object to receive the event and make the decision about what needs to be done. A touch event is usually dispatched to the main window object, which in turn dispatches it to the view in which the touch occurred. Other events might take slightly different paths through various app objects.

Many types of events can be delivered in an iOS app. The most common ones are listed in Table 2-2. Many of these event types are delivered using the main run loop of your app, but some are not. Some events are sent to a delegate object or are passed to a block that you provide. For information about how to handle most types of events—including touch, remote control, motion, accelerometer, and gyroscopic events—see Event Handling Guide for iOS.


During startup, the UIApplicationMain function sets up several key objects and starts the app running. At the heart of every iOS app is the UIApplication object, whose job is to facilitate the interactions between the system and other objects in the app. Figure 2-1 shows the objects commonly found in most apps, while Table 2-1 lists the roles each of those objects plays. The first thing to notice is that iOS apps use a model-view-controller architecture. This pattern separates the app’s data and business logic from the visual presentation of that data. This architecture is crucial to creating apps that can run on different devices with different screen sizes.

The role of objects in an iOS app

UIApplication object:

The UIApplication object manages the event loop and other high-level app behaviors. It also reports key app transitions and some special events (such as incoming push notifications) to its delegate, which is a custom object you define. Use the UIApplication object as is—that is, without subclassing.

App delegate object:

The app delegate is the heart of your custom code. This object works in tandem with the UIApplication object to handle app initialization, state transitions, and many high-level app events. This object is also the only one guaranteed to be present in every app, so it is often used to set up the app’s initial data structures.

Documents and data model objects:

Data model objects store your app’s content and are specific to your app. For example, a banking app might store a database containing financial transactions, whereas a painting app might store an image object or even the sequence of drawing commands that led to the creation of that image. (In the latter case, an image object is still a data object because it is just a container for the image data.)
Apps can also use document objects (custom subclasses of UIDocument) to manage some or all of their data model objects. Document objects are not required but offer a convenient way to group data that belongs in a single file or file package. For more information about documents, see Document-Based App Programming Guide for iOS.

View controller objects:

View controller objects manage the presentation of your app’s content on screen. A view controller manages a single view and its collection of subviews. When presented, the view controller makes its views visible by installing them in the app’s window.
The UIViewController class is the base class for all view controller objects. It provides default functionality for loading views, presenting them, rotating them in response to device rotations, and several other standard system behaviors. UIKit and other frameworks define additional view controller classes to implement standard system interfaces such as the image picker, tab bar interface, and navigation interface.
For detailed information about how to use view controllers, see View Controller Programming Guide for iOS.

UIWindow object:

A UIWindow object coordinates the presentation of one or more views on a screen. Most apps have only one window, which presents content on the main screen, but apps may have an additional window for content displayed on an external display.
To change the content of your app, you use a view controller to change the views displayed in the corresponding window. You never replace the window itself.
In addition to hosting views, windows work with the UIApplication object to deliver events to your views and view controllers.

View objects, control objects, and layer objects:

Views and controls provide the visual representation of your app’s content. A view is an object that draws content in a designated rectangular area and responds to events within that area. Controls are a specialized type of view responsible for implementing familiar interface objects such as buttons, text fields, and toggle switches.
The UIKit framework provides standard views for presenting many different types of content. You can also define your own custom views by subclassing UIView (or its descendants) directly.
In addition to incorporating views and controls, apps can also incorporate Core Animation layers into their view and control hierarchies. Layer objects are actually data objects that represent visual content. Views use layer objects intensively behind the scenes to render their content. You can also add custom layer objects to your interface to implement complex animations and other types of sophisticated visual effects.

Un thread es un "hilo" de ejecucion de programa. Casi podriamos decir que un Thread o hilo es un programa en ejecucion ya que en general un programa tiene un solo hilo de ejecucion. Cuando se ejecuta un programa o el sistema operativo crea un hilo para ejecutar un programa.Treads are a relatively lighteight wat to implement multiple paths of execution inside of an application.
tuple: A grouping of values.
type casting: A way to check the type of an object, and to treat that object as if it's a different superclass or subclass from somewhere else in its own class hierarchy.
type inference: The ability of the Swift compiler to determine the type of a value from context, without an explicit type declaration.
A view controller that manages the system interfaces for taking pictures, recording movies, and choosing items from the user's media library.
A set of methods that your delegate object must implement to interact with the image picker interface.
UIImagePickerControllerOriginalImage: Specifies the original, uncropped image selected by the user.An object that displays a single image or a sequence of animated images in your interface.
UIKit: A Cocoa Touch framework for working with the user interface (UI) layer of an iOS app.
A set of methods that your delegate object must implement to interact with the image picker interface.
An object that manages a view hierarchy for your UIKit app.

A structure that parses URLs into and constructs URLs from their constituent parts.URLSession, a complete networking API for uploading and downloading content via HTTP. URLSession is technically both a class and a suite of classes for handling HTTP/HTTPS-based requests:
underscore: A representation of a wildcard in Swift (_).

unit test: A piece of code written specifically to test a small, self-contained piece of behavior in your app to make sure it behaves correctly.

Unit Testing: is a method for testing individual units (usually a single method) of your app to make sure your app is ready to be released.

unwind segue: A type of segue used to implement backward navigation.

unwrap: To extract an underlying value from an optional.

user interface (UI): The layer of visual elements that lets a user interact with a piece of software.

utility area: An area in Xcode that displays the inspector pane and .

variable: A value that can change after it's been initialized, indicated in Swift by the var keyword.

view: An object that's used to construct your user interface (UI) and display content to the user.

view controller: An object that manages a set of views and coordinates the flow of information between the app's data model and the views that display that data.

view hierarchy: A hierarchical representation of views relative to other views.

workspace window: The Xcode window, which you use to manage and navigate through the files and resources in your project.

action:	A piece of code that's linked to an event that can occur in your app.

activity viewer:	Part of the Xcode toolbar that displays messages about the build process and other information.

adaptive interface: A user interface (UI) that automatically adjusts so that it looks good in the context of the available screen space.

Swift Version

vim hello.swift

app delegate: An object in your app (specifically, an instance of the AppDelegate class) that creates the window where your app's content is drawn and that provides a place to respond to state transitions within the app.

application object: An object in your app that's responsible for managing the life cycle of the app, communicating with its delegate, the app delegate, during state transitions within the app.

argument: A value you pass in to a function, method, or initializer to satisfy one of its parameters.

array: A data type that stores multiple values of the same type in an ordered list.

asset catalog: A tool to manage assets like images that are used by your app as part of its user interface (UI).

assistant editor: In Xcode, a secondary editor window that appears side-by-side with your primary editor.

Attributes inspector: An inspector that you use to customize visual attributes of a user interface (UI) element in a storyboard.

Auto Layout: A layout engine that helps lay out your user interface (UI) based on the constraints you specify.

base class: A class that's at the root of its class hierarchy, meaning that it has no superclass.

struct Settings {
    static let shared = Settings()
    var username: String?

    private init() { }
}
Binding generally refers to a mapping of one thing to another. In the context of software libraries, bindings are wrapper libraries that bridge two programming languages, so that a library written for one language can be used in another language.

Binding of data and functions in one single unit named class is know as encapsulation. Encapsulation provides data hiding facility. In programming languages encapsulation is implemented using classes. Basically binding means to associate data and functions with a particular unit i.e. class. So variable and functions are bind to class means they are related to only the class in which they are declared. To access them outside class one must use object(instance) of that class or class name. So they are bind to the class.canvas: The background of a storyboard where you add and arrange user interface (UI) elements.

class: A piece of code that describes the behavior and properties common to any particular type of object, essentially providing a blueprint for the object.

class hierarchy: A hierarchical representation of a class's relationships to its superclass and subclasses.

clean: Removes all the product files, as well as any object files or other intermediate files created during the build process.

closed range operator: An operator (...) that lets you create a range of numbers that includes both the lower and upper values.
A closure is said to escape a function when the closure is passed as an argument to the function, but it is called after the function returns.

Cocoa Touch: The set of Apple frameworks and technologies used to develop iOS apps.

CocoaPods is a dependency manager for Swift and Objective-C Cocoa projects.

code completion: A feature of Xcode that infers what you're trying to type from context and provides suggestions that you can select.

When you need a different key name

Let’s say for the JSON, you want the key name to be “number_of_legs” (snake cased), instead of “numberOfLegs”.
To customize the JSON key names, add CodingKeys enum to the struct.

struct Animal: Codable {
    var numberOfLegs: Int
    enum CodingKeys: String, CodingKey {
        case numberOfLegs = "number_of_legs"
    }
}4 horas = 1 dia

Asesoramiento
requyerimientos -> $$
documento de analisis de requerimientos funcionales -> $$

not disclosure agreement

cada vista tiene una complejidad

facil = 4 horas
media = 16 horas
complejo = 24 horas
experto = 48 horas

(total de horas)*0.20 = gran total

gran total * (costo de hora)*(1.16)*1.32*0.3

(0.3 asesoria externa)

completion handler: A closure that's passed as a parameter to a method that calls the closure when it finishes executing.
conditional statement: A control flow statement that checks whether a condition is true before executing a piece of code.
conform to: For a class, structure, or enumeration to satisfy the requirements of a protocol.
Steps you do before:
- Access NASA APOD API
- Check for a response
- convert the response body to string
- print the string

what is next ? use JSONDecoder to convert the response to native Swift types.

CONVERT JSON DATA TO SWIFT TYPES

- Instances of JSONDecoder have a decode(_:from:) method
- JSONDecoder accepts parameters of type Type
- JSONDecoder accepts another parameter of type Data.

JSONDecoder's decode () method is considered a throwing function, which you have encountered before. Remember that by the pairing a throwing function with the do-try-catch syntax, you can capture and address each specific error that the mothod can throw.

More simply, if you procede a throwing function with try?, the function will return an optional value.
tthe function will return an optional value, If there is no error, the optional will hold the expected value, if there is an error, the optional will be nil.

in your playground, use JSONDecoder to decode the data returned to you frm the API into dictionary [String:String]. Since String already conforms to Codable, you do not need to do anything special involving Codable. 

let task = URLSession.shared.dataTask(with: url) { (data, response, error) in
	if let data = data, 
					let photoDictionary = try? jsonDecoder.decode([String: String].self, from: data) {
			print(photoDictionary)
}
task.resume()

REMEMBER:
- String already conforms to Codable.
- JSONDecoder has a mapping that it can follow to convert from JSON with string values to a Swift dictionary with the keys of type String and values of type String.


You create simple singletons using a static type property, which is guaranteed to be lazily initialized only once, even when accessed across multiple threads simultaneously:

class Singleton {
    static let sharedInstance = Singleton()
}

If you need to perform additional setup beyond initialization, you can assign the result of the invocation of a closure to the global constant:

class Singleton {
    static let sharedInstance: Singleton = {
        let instance = Singleton()
        // setup code
        return instance
    }()
}
what did you do before ?
- serialize JSON data into native Swift types.

You have to prepare to serialize the data into your own custom model objects.

{
  "date": "2017-02-13",
  "explanation": "Juno just completed its fourth pass near
  Jupiter...",
  "hdurl": "http://apod.nasa.gov/apod/image/1702/JupiterSouth_JunoPeach_1200.jpg",
  "media_type": "image",
  "service_version": "v1",
  "title": "Cloud Swirls around Southern Jupiter from Juno",
  "url": "http://apod.nasa.gov/apod/image/1702/
  JupiterSouth_JunoPeach_960.jpg"
}

struct PhotoInfo {
	var title: String
	var description: String
	var url: URL
	var copyright: String?
}


A design pattern is the hability to reuse ideas.

This method is called when the app receives a memory warning from the system. It is used to free memory and avoid our app being terminated.To compile and run separately, use swiftc: $ swiftc hello.swift

$ swift hello.swift

This will compile your code into hello file. To run it, enter ./, followed by a filename.

Hello, world!

$ ./hello
Hello, world!

      // an object cannot be initialized until all of its non-optional properties are given a value
    // but in some cases, particularly with iOS development, some properties are nil for just a moment
    // until the value can be specified after initialization.
    // for example you have used Interface Builder to create outlets so that you can access a particular piece
    // of the interface in code.

    @IBOutlet weak var label: UILabel!
    
    // if you were the developer of this class, you would know that anytime a ViewController is created and presented to the user there will always be a label on the screen, because you added it in the storyboard.
    // but in iOS development, the storyBoards elements are not connected to their corresponding outlets until after initialization takes place.
    // therefore, label must be allowed to be nil for a brief period.

    // what about using a regular optional, UILabel?, for the type ?, The standard optional will require the if-let syntax to constantly unwrap the value, providing a safely mechanism for data that may not exist. But you know the label will have a value after the storyboard connects the outlets, so unwrapping an optional that is not really "optional" feels cumbersome.
    // To get around this issue, Swift provides syntax for an implicitly unwrapped optional, using the exclamation mark !, insted the question mark ?. As the name suggest, this type of optional unwraps automatically, whener it is used in code. This allows you to use label as though it were not an optional, while allowing the ViewController to be initialized without it.
    
    // implicitly unwrapped optionals should be used in one special case: when you need to initialize an object without supplying the value , but you know you will be giving the object a value very soon afterwards. It might seem convinient to reach for the implicitly unwrapped optional to save yourself from using if-let syntax, but by doing so you would remove one of the most important safety features of the language.what have you done ?
- performe the request
- decoding JSON data into native swift types you have a dictionary [String:String]
- now you have to convert the dictionary into a PhotoInfo object that you can use thoughout your project.

Codable protocol defines a set of rules that can be applied to a clas or structure that allow you to easily convert data from one to another.

in this case JSONDecoder class can be used to translate information from JSON into your custom model objects.

- encoders and decoders work with Codable types
- init(with:) which is used to initialize the new type of data from the old data
- decode(to:) which is used to convert the current type to a new type of data.
- by default, the Codable protocol matches property names and values with the keys and values of the encoded type. HOwever, in this case you have keys in your JSON data that differ from the names of your properties, which will require you to implement custome keys.
- to map non-matching keys to your properties you need to declare a nested enumeration named CodingKeys that conforms to the CodingKey protocol inside your object. 

Example: 

struct Report: Codable {
	let creationDate: Date
	let profileID: String
	let readCount: Int

	enum CodingKeys: String, CodingKey {
		case creationDate = "report_date"
		case profileID = "profile_id"
		case readCount = "read_count"
	}
}

the JSON data also contains key/value pairs for date, service version, and media type that PhotoInfo does not use. By Default, encoders and decoders that work with Codable objects require that each key or property have a counterpart. To override this, you will need to create your won implementation of the init(from:) method.

Start with the custom keys. The map non-matching keys to your properties you need to declare anested enumeration inside your object named CodingKeys that conforms to the CodingKey protocol.
Each case should correspond to a property and have the same as the property. If the property name and the name of the key in the data differ, you will need to assign an associate String to the case where the value is the same as the key name in the data.

For example: PhotoInfo has a property called description that should map to the NASA APOD API explanation key. Your enum should includ a case for description that is set equal to "explanation". The keys that match do not need an associated value. When finished, your enumeration should look something like the following:

enum CodingKeys: String, CodingKey {
	case title
	case description = "explanation"
	case url
	case copyright
}

while you are one step closer to being able to decode your JSON data to a PhotoInfo object, you still need to implement your own version of init(from:) that ignores the extrangeous key/value pairs in the data that PhotoInfo will not include. Start by declaring an initializer inside of PhotoInfo as follows:

init(from decoder: Decoder) throws {
}

the throws keyword indicates that this initializer is a throwing function. This initializer will not be called by you directly, but by the Decoder that you use to decode your JSON data, so errors will be handle by the Decoder object or passed along when you call the decode(_:from:) method.

Inside the initializer, you need to access the JSON data´s key/value pairs through decoder. You first do this by accessing a KeyedCodingContainer, which acts much like a dictionary. Do this with the code let valueContainer = try decoder.container(keyedBy: CodingKeys.self). This wil return a KeyedCodingContainer that only contaiuns the key/value pairs associated with the cases declared in CodingKeys.

Once you have done this, you can use the decode(_:from:) method provided by the KeyedCodingContainer object to get each of the values corresponding to the keys you want and assign them to the correct properties. For example: you could type self.title = try values.decode(String.self, forkey: CodingKeys.title). Do this for all fo the properties. You Should end up with an initializer that looks like the following:

init(from decoder: Decoder) throws {
	let valueContainer = try decoder.container(keyedBy: CodingKeys.self)
	self.title = try valueContainer.decode(String.self, forKey: CodingKeys.title)
	self.description = try valueContainer.decode(String.self, forKey: CodingKeys.description)
	self.url = try valueContainer.decode(URL.self, forkey: CodingKeys.url)
	self.copyright = try? valueContainer.decode(String.self, forKey: CodingKeys.copyright)
}

Altogether, your PhotoInfo object should include its properties, an enumeration called CodingKeys, and an initializer called init(from:). It should look like this:

struct PhotoInfo: Codable {
	var title: String
	var description: String
	var url: URL
	var copyright: String?

	enum CodingKeys: String, CodingKey {
		case title
		case description = "explanation"
		case url
		case copyright
	}
	init(from decoder: Decoder) throws {
		let valueContainer = try decoder.container(keyedBy: CodingKeys.self)
		self.title = try valueContainer.decode(String.self, forKey: CodingKeys.description)
		self.description = try valueContainer.decode(String.self, forKey: CodingKeys.description)
		self.url = try valueContainer.decode(String.self, forKey:CodingKeys.copyright)
	}
}

# vim: syntax=conf
# Keychain for iOS

“…an encrypted container that securely stores small chunks of data on behalf of apps and secure services.
and
…simply a database stored in the file system.”
It is written in C and requires a lot of time-consuming configuration.
Luckily, Apple and many other contributors have created higher level wrappers to hide the convoluted C code and organization powering things from beneath.
* Implementation with Wrappers

-  GenericKeychain (apple's own keychain)
- other wrappers exist as cocoapods or extension libraries on GitHub and other dependency management sites.
			- keychain
			- SAMkeychain
			- KeychainSwift
			- RGSwiftKeychain
			- swiftkeyChainWrapper

origin : The starting coordinate (0,0,0) that can be used to position objects.

- Will anything else own, manage or be responsible for it?
- Is there going to be exactly one instance?
- Will it be a global state variable?
- Should I really use a globally shared object?
- Should live through the whole app lifecycle?
- Is there any alternatives for it?
scene: A storyboard representation of a screen of content in your app.
Static KeyWord: To ensure that the constants are defined only one time and are not tied to a particular instance of your model, use the static keyword. example: static let DocumentDirectory
Type Casting: is a way to treat an instance as if it were a different class in its inheritence chain.

When you treat an instance as if it were a class higher up in the inheretence chain, it is called upcasting
When you treat an instance as if it were a class farther down in the inherentence chain, it is called downcasting.
var etiqueta: UILabel = UILabel()
var vista: UIView = etiqueta as UIView

var vistaEtiqueta: UIView = UILabel()
var etiquetavista: UILabel = vistaEtiqueta as! UILabelyou now have an initializer for the photoInfo type that the JSONDecoder can use to decode JSON into a PhotoInfo object. Next, you will need to update the completion handler in your network request so the it uses the new type instead of printing the json value. Add a line to your if-let check to initialize an instance of PhotoInfo, then print the value:

let task = URLSession.shared.dataTask(with: url) { (data, response, error) in
				let jsonDecoder = JSONDecoder()

$  swift
Welcome to Apple Swift. Type :help for assistance.
  1> func greet(name: String, surname: String) {
  2.     print("Greetings \(name) \(surname)")
  3. }
  4>
  5> let myName = "Homer"
myName: String = "Homer"
  6> let mySurname = "Simpson"
mySurname: String = "Simpson"
  7> greet(name: myName, surname: mySurname)
Greetings Homer Simpson
8> ^DThis method is called after the main view is removed from the screen.
This method is called after the main view has been removed from the screen.This method is called after the main view and its content ios loaded in memory. It is the first method called on the object to indicate that the main view is ready to be shown on the screen.This method is called after the viewDidLoad() method and before the main view is shown on the screen.This method is called before the main view is removed from the screen.- it's a very popular and commonly adopted pattern because of simplicity. 
- A singleton class can only have exactly one instance through the entire application lifecycle. 
- That single instance is only accessible through a static property and the initialized object is usually shared globally. 
-  It's like a global variable. 🌏
What Is A Type?
First things first. The Swift programming language uses types, like classes and structs, to represent different kinds of data in your app’s code.

Some examples:

Int is used for integer values, or “whole numbers”
Double is used for decimal-point values, like 3.1415
String is used for text, like "Tinker Tailor Soldier Spy"
UIButton is used for a button user interface element

When referring to a database or search, a query is a field or option used to locate information within a database or another location.
