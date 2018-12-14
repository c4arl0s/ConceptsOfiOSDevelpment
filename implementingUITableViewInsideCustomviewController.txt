class viewController: UIViewController, UITableViewDelegate, UITableViewDataSource {

    let tableView = UITableView()    

    override func viewDidLoad {
      tableView.delegate = self			// it has to send the messages to self
      tableView.dataSource = self		
    }
