# iOS_FootballMatchesApp_Tutorial

First, congrats on making it this far. If you're here, then you've encountered JSON file parsing, Constraints, and basic app functionalities. The goal of this app is to get you started on more complex concepts, namely, API calls. 

API stands for Application Program Interface. An API makes it easier to develop an iOS app, or any application in general because it provides all the building blocks that we programmers use. More concretely, APIs are used all the time in most websites. Think about it, every time you get a movie ticket, you go on the website and you enter all your information, credit card and then you print your tickets. APIs fill in the blankets between you entering the information and getting your ticket. They handle payment, movie tickets left and so on. 

So an API is a big system that does a lot of things for us. Luckily, as we begin our journey in iOS, we don't need to know *how to make an API*, just how to use one, or the more appropriate expression is: how to **call an API**, in turn receiving information from some website or service. In our case, the service will be an API that provides Football Match Information and returns **text data** for us to use.  

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/1.png" width="50%" height="50%">

**Let's Start.**

# First steps: Setting up Project
You should know this by now! Make a new project, give your app a creative name and let's get started. If you forgot how to do this, look at previous tutorials. 

## Second step: Creating the UI Part

Let's start by designing the Football App User Interface (UI). In this App we use UITableview to show all the dynamic data in rows. **UITableView** is a UI structure that shows a table with rows (consider alarm app for example). Each row in a TableView is called **UITableViewCell**. These cells contain **UIlabels** showing the data which is coming from the server dynamically.

Select Main.Storyboard file and start designing your app. There is a view in Main.Storyboard named **View Controller Scene**. This class is the main view of the application that the user interacts with. You can see a **+** button on the top.  Click on that button.  A small window will pop up, in which all the design elements are available. Search for the UITableView and drag and drop the UITableView to the View Controller. The View should look like this:

<p float="center">
  <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/2.png" width="50%" height="50%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/3.png" width="50%" height="50%">
</p>

Select the UITableView and add constraints of value 0 on all sides. We definitely want this TableView to be centered and well positioned. Next, we add a Prototype cell in UITableview from attribute Inspector.**What is Prototype Cell?**
**Prototype cells are a way to layout the look and feel of a cell inside a table view, they allow us to get a representation of how things are going to work when the application runs and data is passed into the table.**

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/4.png">

Now design the cell with UILabels. Now go to **+** button and drag drop UILabels. Change colors and fonts like we did in **Calculator Tutorial** and set all the constraints. It should look as follows:

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/5.png">

Now add a Tableview Cell class in which we set IBOutlets of UILabels of cell. By default, a UITableViewCell only contains a title label and a text label. In order to have more custom elements, such as all the labels we habe in our project, we need to make a custom UITableViewCell where we intergrate all the elements as IBOutlets. 

To implement this, go to **Project Navigator** -> **Right Click** -> **Select NewFile** -> **Cocoa Touch Class** -> **Set Class Name** -> **Subclass of UITableViewCell** -> **Language Swift** (check out the screenshot for more info).

Next. just go to **Main.storyboard** file and select **cell** then goto **Identity Inspector** and set **Class** your **cell class name**

<p float="center">
  <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/6.png" width="45%" height="45%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/7.png" width="45%" height="45%">
  <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/8.png" width="45%" height="45%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/9.png" width="45%" height="45%">
</p>

Now add UILabels @IBOutlet in **MatchTVC** like we did in **Calculator Tutorial** and connect with cell.

<p float="center">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/10.png" width="45%" height="45%">
 <img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/11.png" width="45%" height="45%">
</p>

Now It's time to run the Application with static Table View Content. For this, Add Table View @IBOutlet in ViewController Class. Use TableView **Delegates & DataSource** to show the **Number of rows** and **Display Reusable cells**.

### What is TableView Delegates & DataSource

Datasource methods are used to generate tableView cells, header and footer before they are displayed. Delegate methods provide information about these cells, header and footer along with other user action handlers like cell selection and edit.

# Delegates & DataSource

``
      func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        
      } 
  ``
        
*tableView:numberOfRowsInSection*: Tells the data source to return the number of rows in a given section of a table view.


``
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
  
  }
  ``

This is a DataSource method so it will be called on whichever object has declared itself as the DataSource of the UITableView. It is called when the table view actually needs to display the cell onscreen, based on the number of rows and sections (which you specify in other DataSource methods).

Now create an **Extension** in ViewController Class and add TableView Delegates & DataSource.
  
**Extensions** add new functionality to an existing class, structure, enumeration, or protocol type. This includes the ability to extend types for which you do not have access to the original source code.
viewController Class looks like as follows.

<img src="https://github.com/code-techniq/Project6_iOS_FootballMatchesApp_Doc/blob/master/ScreenShots/12.png">

Now create a Reusable Cell object in ``func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {}`` to display the cell on the screen

```
        //Cell Declaration
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! MatchTVC
         return cell
```
**dequeueReusableCell (important)** : For performance reasons, a table view data source should generally reuse UITableViewCell objects when it assigns cells to rows in its tableView(_:cellForRowAt:) method. A table view maintains a queue or list of UITableViewCell objects that the data source has marked for reuse. Call this method from your data source object when asked to provide a new cell for the table view. This method dequeues an existing cell if one is available or creates a new one using the class or nib file you previously registered. If no cell is available for reuse and you did not register a class or nib file, this method returns nil.

Give an Identifier to your cell in Main.storyboard file. Select the cell and then go to the Attributes inspector, change the identifier value there. Pass that identifier to **dequeueReusableCell**. In our case we have given the cells the identifier "cell".

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

Now open ViewController.swift class and `import Alamofire`. Declare URL of Api and an array in which we will sotre the response of Api.

```  
let kBaseUrl = "https://api.football-data.org/v2/competitions/CL/matches" 
```
```
var matchesList = [[String : AnyObject]]()

```
# API Call
  Now make a function in which we call the Api and get the response and store in the array. call that function in Viewontroller.swift's  **View life cycle** method **viewDidLoad**. Now we need to check the internet connection. If Internet connection is available then we call the Api otherwise we will show the alert that Internet connection is not available 
 **Check Internet connection**
 ```
 if !NetworkReachabilityManager()!.isReachable {
            
            let alert = UIAlertController(title: "Alert", message: "No Internet Connection", preferredStyle: UIAlertController.Style.alert)
            alert.addAction(UIAlertAction(title: "Click", style: UIAlertAction.Style.default, handler: nil))
            self.present(alert, animated: true, completion: nil)
            return
            
        }
 ```
  
  If internet is avaialble then in `else` condition call the Api.
  ```
  else {
            let header: [String: String] = ["X-Auth-Token":"d082ae8b70b442de84e52a1804c39e9e"]
            request(kBaseUrl, method: .get, parameters: nil, encoding: JSONEncoding.default, headers: header)
                .responseJSON { response in
                    switch response.result {
                    case .success(_):
                    if let apiData = response.result.value as? NSDictionary {
                    if let data = apiData["competition"] as? [String : AnyObject] {
                        self.leagueNameLbl.text = data["name"] as? String ?? ""
                                }
                        if let matches = apiData["matches"] as? [[String : AnyObject]] {
                            for match in matches {
                                    self.matchesList.append(match)
                                        }
                                    }
                                    self.matchList_TableView.reloadData()
                                }
                    case .failure(let error):
                        print(error.localizedDescription)
              }
            }
          }
  ```
  above code is used for calling the Api. We have used Authorization Token in Header. Why we use Header?
  
  The HTTP Authorization request header contains the credentials to authenticate a user agent with a server, usually after the server has responded with a 401 Unauthorized status.
  
  following method is used to call the Api and get the reponse
  
  ```
  request(kBaseUrl, method: .get, parameters: nil, encoding: JSONEncoding.default, headers: header)
                .responseJSON { response in
                    switch response.result {
                    case .success(_):
  ```
Now first thing you need to do is print the response and analyse the response. Store the data that you need to display on Table.
```
                    if let apiData = response.result.value as? NSDictionary {
                    if let data = apiData["competition"] as? [String : AnyObject] {
                        self.leagueNameLbl.text = data["name"] as? String ?? ""
                                }
                        if let matches = apiData["matches"] as? [[String : AnyObject]] {
                            for match in matches {
                                self.matchesList.append(match)
                                        }
                                    }
                                    self.matchList_TableView.reloadData()
                                }

```
at the end reload the tableview so that all the data on table should be dynamic. 

# Set Table content dynamically

First thing is to give number of rows dynamically according to the array count.

```
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return matchesList.count
    }
```

**Display Api data on the Cell**

```
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        
        //Cell Declaration
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! MatchTVC
        
        //Parsing Data From The Json Object (from inspirator JSON project)
        let score = matchesList[indexPath.row]["score"] as? [String : AnyObject] ?? [String : AnyObject]()
        let homeTeam = matchesList[indexPath.row]["homeTeam"] as? [String : AnyObject] ?? [String : AnyObject]()
        let homeTeamName = homeTeam["name"] as? String ?? ""
        
        //Fill in the cell properties (labels)
        let fullTime = score["fullTime"] as? [String : AnyObject] ?? [String : AnyObject]()
        let homeTeamScore = fullTime["homeTeam"] as? Int ?? 0
        let awayTeamcore = fullTime["awayTeam"] as? Int ?? 0
        cell.leagueTitleLbl.text = matchesList[indexPath.row]["group"] as? String ?? ""
        cell.dateLbl.text = matchesList[indexPath.row]["utcDate"] as? String ?? ""
        cell.team1NameLbl.text = homeTeamName
        return cell
        }
```

Thats It! Now you can get a response from any API and display it on your TableView! 
