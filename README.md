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

