# iOS_FootballMatchesApp_Tutorial

This will be a beginner's tutorial for making an App with json parsing using API on the iPhone. All the basic concepts will be explained. We are going to make an App in which we get the **text data** from server using API and show that data on a Table View.Here It's look like. 

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/1.png" width="50%" height="50%">

**Let's Start.**

# First steps: Setting up Project
Create a new project and setup like we did previously in **Calculator App**. This step is similer with that App

## Second step: Creating the UI Part

Let's start to design the Football App UI. In this App we use UITableview to show all the dynamic data in rows.In Table View we add a UITableViewCell in Which we add UIlabels to print the data, which is coming from server dynamically.

just go to the Main.Storyboard file and start designing your app. There is a view in Main.Storyboard named **View Controller Scene**. This class is the main view of the application that the user interacts with. You can see a **+** button on the top.  Click on that button.  A small window will pop up, in which all the design elements are available. Search for the UITableView and drag and drop the UITableView to the View Controller. The View should look like this:

<p float="center">
  <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/2.png" width="50%" height="50%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/3.png" width="50%" height="50%">
</p>

After adding UITableview, add Prototype cell in UITableview from attribute Inspector.**What is Prototype Cell?**
**Prototype cells are a way to layout the look and feel of a cell inside a table view, they allow us to get a representation of how things are going to work when the application runs and data is passed into the table.**

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/4.png">

Now design the cell with UILabels. Now go to **+** button and drag drop UILabels. Change colors and fonts like we did in **Calculator Tutorial** and set all the constraints. View look like as follow.

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/5.png">

Now add a Tableview Cell class in which we set IBOutlets of UILabels of cell.
Go to **Project Navigator** -> **Right Click** -> **Select NewFile** -> **Cocoa Touch Class** -> **Set Class Name** -> **Subclass of UITbaleViewCell** -> **Language Swift**. Look like as follows. Then just go to **Main.storyboard** file and select **cell** then goto **Identity Inspector** and set **Class** your **cell class name**
<p float="center">
  <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/6.png" width="45%" height="45%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/7.png" width="45%" height="45%">
  <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/8.png" width="45%" height="45%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/9.png" width="45%" height="45%">
</p>

Now add UILabel's @IBOutlet in **MatchTVC** like we did in **Calculator Tutorial** and connect with cell.

<p float="center">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/10.png" width="45%" height="45%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/11.png" width="45%" height="45%">
</p>

Now It's time to run the Application with static Table View Content. For this, Add Table View @IBOutlet in ViewController Class. Use TableView **Delegates & DataSource** to show the **Number of rows** and **Display Reusable cells**.
**What is TableView Delegates & DataSource**
Datasource methods are used to generate tableView cells,header and footer before they are displaying.Delegate methods provide information about these cells, header and footer along with other user action handlers like cell selection and edit.
# Delegates & DataSource
**func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        }**
tableView:numberOfRowsInSection: Tells the data source to return the number of rows in a given section of a table view.


**func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {}**
This is a DataSource method so it will be called on whichever object has declared itself as the DataSource of the UITableView. It is called when the table view actually needs to display the cell onscreen, based on the number of rows and sections (which you specify in other DataSource methods).

Now create an **Extension** in ViewController Class and add TableView Delegates & DataSource.
  
**Extensions** add new functionality to an existing class, structure, enumeration, or protocol type. This includes the ability to extend types for which you do not have access to the original source code.
viewController Class looks like as follows.

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/12.png">

Now create a Reusable Cell object in **func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {}** to display the cell on the screen

```
        //Cell Declaration
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! MatchTVC
         return cell
```
**dequeueReusableCell**: For performance reasons, a table view data source should generally reuse UITableViewCell objects when it assigns cells to rows in its tableView(_:cellForRowAt:) method. A table view maintains a queue or list of UITableViewCell objects that the data source has marked for reuse. Call this method from your data source object when asked to provide a new cell for the table view. This method dequeues an existing cell if one is available or creates a new one using the class or nib file you previously registered. If no cell is available for reuse and you did not register a class or nib file, this method returns nil.

Give an Idenifire to your cell in main.storyboard file and pass that Identifire to **dequeueReusableCell** like above We have given Identifire "cell".

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/13.png">

Now run the App. It will show static TableView on the Screen. Next step is to Hit an API and get data from server and set that data on Table and make it dynamic . Before moving forward Let's discuss that What is an API?

**API**: An application programming interface (API) is an interface or communication protocol between a client and a server intended to simplify the building of client-side software. It has been described as a “contract” between the client and the server, such that if the client makes a request in a specific format, it will always get a response in a specific format or initiate a defined action.
Following is a format of an API
```
"https://api.football-data.org/v2/competitions/CL/matches"
```
To download the content from server we use **Alamofire** Network Library.

Why do you need Alamofire at all? Apple already provides URLSession and other classes for downloading content via HTTP, so why complicate things with another third party library?

The short answer is Alamofire is based on URLSession, but it frees you from writing boilerplate code which makes writing networking code much easier. You can access data on the Internet with very little effort, and your code will be much cleaner and easier to read.

We add **Alamofire** dependency using **Cocoa pods** . Add pod file in your project using following link:
[Install Cocoa pods](https://guides.cocoapods.org/using/using-cocoapods.html)

After add cocoa pods please open your workspace file . You will see an another project in you existing project. Now open uor pod file and write following lines to add dependeces of third party libraries. We are using two libraries
```
target 'Football Matches' do
  
  use_frameworks!

  pod 'Alamofire'
  pod 'ReachabilitySwift', :inhibit_warnings => true

end
```
1. Alamofire(Networking Library)
2. ReachabilitySwift(Check Internet Connection)

After addition of pod file your project look like as follows.
<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/14.png">


