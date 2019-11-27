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
