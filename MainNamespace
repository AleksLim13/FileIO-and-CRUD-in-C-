using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;



namespace ALim_A1_PROG32356_June13_Spring2021
{
    class Program
    {
        //Declare-Define: 3 file URLs where data comes in and out from slash to 
        const string fVehicle = @".\vehicles.txt";
        const string fInvent = @".\inventory.txt";
        const string fRepair = @".\repairs.txt";

        static void Main(string[] args)
        {
            
            Menu menu = new Menu();
            FileIO data = new FileIO();
            ConvertedLists cvlLists = data.FormatData(fVehicle, fInvent, fRepair);

            string[] vehicles = new string[cvlLists.VList.Length];

            for (int i = 0; i < vehicles.Length; i++) {
                vehicles[i] = cvlLists.VList[i].Make + " " + cvlLists.VList[i].Model + " " + cvlLists.VList[i].Year;
            }//End F:*


            var ascn = from str in vehicles
                       orderby str ascending
                       select str;

            Console.WriteLine("All Vehicles for User Input");
            Console.WriteLine("__________________________");
            foreach (string c in ascn.Distinct())
            {
                Console.WriteLine(c + ",");
            }//End FE:*

            Console.WriteLine("__________________________");

            menu.StartMenu(cvlLists, fVehicle, fInvent, fRepair);



        }//End M:*

    }//End CL:*


    public class Vehicle
    {
        
        private long id;
        private string make;
        private string model;
        private int year;
        private string cond;

        public Vehicle(
                       long id, 
                       string make, 
                       string model, 
                       int year, 
                       string cond
                      )
        {
            this.id = id;
            this.make = make;
            this.model = model;
            this.year = year;
            this.cond = cond;
        }//End C:*

        public long Id
        {
            get { return id; }
            set { id = value; }
        }//End IND:*

        public string Make
        {
            get { return make; }
            set { make = value; }
        }//End IND:*
  
        public string Model
        {
            get { return model; }
            set { model = value; }
        }//End IND:*

        public int Year
        {
            get { return year; }
            set { year = value; }
        }//End IND:*

        public string Cond {
            get { return cond; }
            set { cond = value; }
        }//End IND:*

    }//End CL:*

    public class Inventory
    {
        
        private long id;
        private long vehicleId;
        private int numOnHand;
        private double price;
        private double cost;

        public Inventory(
                         long id, 
                         long vId, 
                         int nOH, 
                         double p, 
                         double c
                       )
        {
            this.id = id;
            this.vehicleId = vId;
            this.numOnHand = nOH;
            this.price = p;
            this.cost = c;

        }//End C:*

       

   
        public long Id
        {
            get { return id; }
            set { id = value; }
        }//End IND:*

        public long VehicleId
        {
            get { return vehicleId; }
            set { vehicleId = value; }
        }//End IND:*


        public int NumOnHand
        {
            get { return numOnHand; }
            set { numOnHand = value; }
        }//End IND:*

        public double Price
        {
            get { return price; }
            set { price = value; }
        }//End IND:*

        public double Cost
        {
            get { return cost; }
            set { cost = value; }
        }//End IND:*

    }//End CL:*

    public class Repair
    {
        
        private long id;
        private long inventId;
        private string whatToRepair;

        public Repair(long id, long iID, string wTR)
        {
            this.id = id;
            this.inventId = iID;
            this.whatToRepair = wTR;
        }//End C:*
 
        public long Id
        {
            get { return id; }
            set { id = value; }
        }//End IND:*

        public long InventId
        {
            get { return inventId; }
            set { inventId = value; }
        }//End IND:*


        public string WhatTo
        {
            get { return whatToRepair; }
            set { whatToRepair = value; }
        }//End IND:*

    }//End CL:*


    public class FileIO {
        public FileIO() { 

        }//End C:*

        public List<List<string>> readAll(string vPath, string iPath, string rPath) {

            List<List<string>> mList = new List<List<string>>();

            try {

                List<string> dynVehicles = new List<string>();
                List<string> dynInventory = new List<string>();
                List<string> dynRepairs = new List<string>();

                string[] vehicles = File.ReadAllLines(vPath);

                for (int i = 0; i < vehicles.Length; i++)
                {
                    dynVehicles.Add(vehicles[i]);
                }//End F:*

                mList.Add(dynVehicles);

                string[] inventory = File.ReadAllLines(iPath);

                for (int i = 0; i < inventory.Length; i++)
                {
                    dynInventory.Add(inventory[i]);
                }//End F:*

                mList.Add(dynInventory);

                string[] repairs = File.ReadAllLines(rPath);

                for (int i = 0; i < repairs.Length; i++)
                {
                    dynRepairs.Add(repairs[i]);
                }//End F:*

                mList.Add(dynRepairs);

                return mList;
            }//End TRY:*

            catch (Exception ex) {
                Console.WriteLine(ex.Message);
            }//End CAT:*

            return mList;
        }//End M:*

        public ConvertedLists FormatData(
                                string fVehicle,
                                string fInvent,
                                string fRepair
                              )
        {
            //Declare-Define: FileIO obj to get data and functionality grouped there. 
            
            ConvertedLists cvlLists = null;

            try {


                //Call-Assign: call readAll of FileIO, pass URLs for each file, assign list of lists to right var.
                FileIO test = new FileIO();
                List<List<string>> mList = test.readAll(fVehicle, fInvent, fRepair);


                //Access-Assign: store right list to right var for futher processing.
                var vehicular = mList[0];
                var inventIt = mList[1];
                var reparations = mList[2];

                //Declare: array to hold multiple vehicle objects.
                Vehicle[] vList = new Vehicle[vehicular.Count];

                //Declare: array of array to store each record as split strings
                string[][] splitVehicular = new string[vehicular.Count][];

                //Recall: id,make,model,year,condition,


                //Repeat: split record, convert necessary items, construct right obj, add to obj array
                for (int i = 0; i < vehicular.Count; i++)
                {
                    splitVehicular[i] = vehicular[i].Split(",");
                    long idTemp = long.Parse(splitVehicular[i][0]);
                    int yearTemp = int.Parse(splitVehicular[i][3]);
                    Vehicle v = new Vehicle(
                                            idTemp,
                                            splitVehicular[i][1],
                                            splitVehicular[i][2],
                                            yearTemp,
                                            splitVehicular[i][4]
                                            );
                    vList[i] = v;

                }//End F:*


                Inventory[] iList = new Inventory[inventIt.Count];
                string[][] splitInventions = new string[inventIt.Count][];
                //Recall: id,vehicleid,numonhand,price,cost,

                //Repeat: split record, convert necessary items, construct right obj, add to obj array
                for (int i = 0; i < inventIt.Count; i++)
                {
                    splitInventions[i] = inventIt[i].Split(",");
                    long idTemp = long.Parse(splitInventions[i][0]);
                    long vIdTemp = long.Parse(splitInventions[i][1]);
                    int nohTemp = int.Parse(splitInventions[i][2]);
                    double pTemp = double.Parse(splitInventions[i][3]);
                    double cTemp = double.Parse(splitInventions[i][4]);
                    Inventory iObj = new Inventory(idTemp, vIdTemp, nohTemp, pTemp, cTemp);
                    iList[i] = iObj;

                }//End F:*



                Repair[] rList = new Repair[reparations.Count];
                string[][] splitReparations = new string[reparations.Count][];
                //Recall: id,inventoryid,whattorepair,



                //Repeat: split record, convert necessary items, construct right obj, add to obj array
                for (int i = 0; i < reparations.Count; i++)
                {
                    splitReparations[i] = reparations[i].Split(",");
                    long idTemp = long.Parse(splitReparations[i][0]);
                    long invIdTemp = long.Parse(splitReparations[i][1]);
                    Repair r = new Repair(idTemp, invIdTemp, splitReparations[i][2]);
                    rList[i] = r;

                }//End F:*


                //Declare-Define: construct ConvertedLists obj to bring back all 3 lists at once.
                cvlLists = new ConvertedLists(vList, iList, rList);

                //Copy: bring back the ConvertedLists obj with fields initialized to what we did above.
                return cvlLists;
            }
            catch (Exception ex) {
                Console.WriteLine(ex.Message);
            }//End CAT:*

            return cvlLists;
        }//End M:*

  
        private string path;
        public string Path
        {
            get { return path; }
            set { path = value; }
        }//End IND:*

        public void SaveAll(ConvertedLists cvlLists, string vP, string iP, string rP) {

            try {

                Vehicle[] vList = cvlLists.VList;
                string[] strVList = new string[vList.Length];
                //Recall: id,make,model,year,condition,
                for (int i = 0; i < strVList.Length; i++)
                {
                    string recordTemp =
                                        vList[i].Id +
                                        "," +
                                        vList[i].Make +
                                        "," +
                                        vList[i].Model +
                                        "," +
                                        vList[i].Year +
                                        "," +
                                        vList[i].Cond +
                                        ",";
                    strVList[i] = recordTemp;
                }//End F:*

                File.WriteAllLines(vP, strVList);

                Inventory[] iList = cvlLists.IList;
                string[] strIList = new string[iList.Length];
                //Recall: id,vehicleid,numonhand,price,cost,
                for (int i = 0; i < strIList.Length; i++)
                {
                    string recordTemp =
                                       iList[i].Id +
                                       "," +
                                       iList[i].VehicleId +
                                       "," +
                                       iList[i].NumOnHand +
                                       "," +
                                       iList[i].Price +
                                       "," +
                                       iList[i].Cost +
                                       ",";
                    strIList[i] = recordTemp;
                }//End F:*

                File.WriteAllLines(iP, strIList);

                Repair[] rList = cvlLists.RList;
                string[] strRList = new string[rList.Length];
                //Recall: id,inventoryid,whattorepair,
                for (int i = 0; i < strRList.Length; i++)
                {
                    string recordTemp =
                                       rList[i].Id +
                                       "," +
                                       rList[i].InventId +
                                       "," +
                                       rList[i].WhatTo +
                                       ",";

                    strRList[i] = recordTemp;
                }//End F:*

                File.WriteAllLines(rP, strRList);
            }
            catch (Exception ex) {
                Console.WriteLine(ex.Message);
            }//End CAT:*

        }//End M:*
    }//End CL:*

    public class ConvertedLists {

        private Vehicle[] vList;
        private Inventory[] iList;
        private Repair[] rList;

        public ConvertedLists() { 

        }//End C:*

        public ConvertedLists(
                              Vehicle[] vList,
                              Inventory[] iList,
                              Repair[] rList
                              ) {
            this.vList = vList;
            this.iList = iList;
            this.rList = rList; 

        }//End C:*

        public Vehicle[] VList
        {
            get { return vList; }
            set { vList = value; }
        }//End IND:*

        public Inventory[] IList
        {
            get { return iList; }
            set { iList = value; }
        }//End IND:*

        public Repair[] RList
        {
            get { return rList; }
            set { rList = value; }
        }//End IND:*

    }//End CL:*


    public class Menu {
        public Menu() { 

        }//End C:*

        public int MainMenu() {
            
            int uChoice = 0;
            
            try {
                Console.WriteLine(
                    "Welcome to Alexandria 24/7 Automotive\n"+
                    "Menu options range from 1-4 and expect an appropriate integer as an input response\n" +
                    "1: Modify Vehicles, 2: Modify Inventory, 3: Modify Repair, 4: Exit Program");

                uChoice = int.Parse(Console.ReadLine());

                return uChoice;
            }//End TRY:*

            catch (Exception ex) {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

            return uChoice;
        }//End M:*

        public int VehicleMenu() {
            
            int uChoice = 0; 
            
            try {
                Console.WriteLine(
                    "You selected Modify Vehicles\n" +
                    "Menu options range from 1-5 and expect an appropriate integer as an input response\n" +
                    "1: List Vehicles, 2: Add Vehicle, 3: Find Vehicle, 4: Delete Vehicle, 5: Return Previous Menu");
                uChoice = int.Parse(Console.ReadLine());
                return uChoice; 
            }//End TRY:*
            catch (Exception ex) {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

            return uChoice; 
        }//End M:*

        public void ListVehicles(ConvertedLists cvlLists) {
            Vehicle[] vList = cvlLists.VList;
            for (int i = 0; i < vList.Length; i++) {
                Console.WriteLine(
                                    "Year: " + 
                                    vList[i].Year + 
                                    ", Make: " + 
                                    vList[i].Make + 
                                    ", Model: " + 
                                    vList[i].Model +
                                    ", Condition: " +
                                    vList[i].Cond
                                   );
            }//End F:*
        }//End M:*

        public void AddVehicle(ConvertedLists cvlLists) {
            
        
            try {

                Vehicle[] vList = cvlLists.VList;
                Inventory[] iList = cvlLists.IList;

                long idTemp = vList.Length + 1;

                Console.WriteLine("Enter the make of the vehicle");
                string makeTemp = Console.ReadLine();

                Console.WriteLine("Enter the model of the vehicle");
                string modelTemp = Console.ReadLine();

                int yearTemp;

                Console.WriteLine("Enter the year of the vehicle");
                yearTemp = int.Parse(Console.ReadLine());

                Console.WriteLine("Enter the condition of the vehicle. E.g., new/used");
                string condTemp = Console.ReadLine();

                Console.WriteLine("What is the price of the vehicle? Expected input [0-9].");
                double uPrice = double.Parse(Console.ReadLine());

                Console.WriteLine("What is the cost of the vehicle? Expected input [0-9].");
                double uCost = double.Parse(Console.ReadLine());

                Console.WriteLine("What is the quantity of the vehicle? Expected input [0-9].");
                int uQuantity = int.Parse(Console.ReadLine());

                Vehicle newV = new Vehicle(
                                           idTemp,
                                           makeTemp,
                                           modelTemp,
                                           yearTemp,
                                           condTemp
                                           );

                Vehicle[] newVList = new Vehicle[vList.Length + 1];
                
                for (int i = 0; i < newVList.Length - 1; i++)
                {
                    newVList[i] = vList[i];
                }//End F:*

                newVList[newVList.Length - 1] = newV;

                cvlLists.VList = newVList;

                Inventory[] newIList = new Inventory[iList.Length + 1];

                Inventory newI = new Inventory(
                    iList[iList.Length - 1].Id + 1,
                    newV.Id,
                    uQuantity,
                    uPrice,
                    uCost);

                for (int i = 0; i < iList.Length; i++) {
                    newIList[i] = iList[i];
                }//End F:*

                newIList[newIList.Length - 1] = newI;

                cvlLists.IList = newIList;

            }//End TRY:*

            catch (Exception ex)
            {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

        
        }//End M:*

        public void FindVehicle(ConvertedLists cvlLists) {

            Vehicle[] vList = cvlLists.VList;

            try {
                
                Console.WriteLine("You selected Find Vehicle \n" +
                    "What is the make of the vehicle your lookigng for? Expecting input [a-z]");
                string uMake = Console.ReadLine();
                
                Console.WriteLine("What is the model of the vehicle your lookigng for? Expecting input [a-z]");
                string uModel = Console.ReadLine();
                
                Console.WriteLine("What is the year of the vehicle your lookigng for? Expecting input [0-9]");
                int uYear = int.Parse(Console.ReadLine());

                for (int i = 0; i < vList.Length; i++) {
                    if (vList[i].Year == uYear && vList[i].Make == uMake && vList[i].Model == uModel) {
                        Console.WriteLine(
                            "Success, A match was found. " +
                            "\n" +
                            "Year: " + 
                            vList[i].Year + 
                            ", Make: " + 
                            vList[i].Make + 
                            ", Model: " + 
                            vList[i].Model
                            );
                    }//End I:*

                }//End F:*

            }//End TRY:*
            catch (Exception ex)
            {
                Console.WriteLine("Input type mismatch exception" + ex.Message);
            }//End CAT:*
            
          
        }//End M:*

        public void DeleteVehicle(ConvertedLists cvlLists) {
            
            Vehicle[] vList = cvlLists.VList;

            try {
                
                Console.WriteLine("You selected Delete Vehicle \n"+
                    "What is the make of the vehicle your looking to delete? Expecting input [a-z]");
                string uMake = Console.ReadLine();

                Console.WriteLine("What is the model of the vehicle your looking to delete? Expecting input [a-z]");
                string uModel = Console.ReadLine();

                Console.WriteLine("What is the year of the vehicle your looking to delete? Expecting input [0-9]");
                int uYear = int.Parse(Console.ReadLine());

                for (int i = 0; i < vList.Length; i++)
                {
                    if (vList[i].Year == uYear && vList[i].Make == uMake && vList[i].Model == uModel)
                    {

               
                        Vehicle[] newVList = new Vehicle[vList.Length - 1];
                       
                        for (int j = 0; j < i; j++) {
                            newVList[j] = vList[j]; 
                        }//End I:*

                 
                        int counter = i + 1;
                       
                        for (int j = i; j < newVList.Length; j++) {
                            newVList[j] = vList[counter];
                            newVList[j].Id = newVList[j].Id - 1;
                            counter++;
                        }//End F:*

                        cvlLists.VList = newVList;


                        Console.WriteLine(
                                       "Success. " +
                                       vList[i].Year +
                                       ", " +
                                       vList[i].Make +
                                       ", " +
                                       vList[i].Model +
                                       " has been deleted."
                                       );

                    }//End I:*

                   
                }//End F:*

            }//End TRY:*

            catch (Exception ex) {
                Console.WriteLine("Input type mismatch exception" + ex.Message);
            }//End CAT:*

        }//End M:*

        public int InventoryMenu()
        {
            int uChoice = 0;
            
            try {
                Console.WriteLine(
                "You selected Modify Inventory\n" +
                "Menu options range from 1-5 and expect an appropriate integer as an input response\n"+
                "1: List Inventory, 2: Add Inventory Item, 3: Find Inventory Item, 4: Delete Inventory Item, 5: Return Previous Menu");
                uChoice = int.Parse(Console.ReadLine());
                return uChoice;
            }//End TRY:*
            
            catch (Exception ex)
            {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*
            
            return uChoice;
        }//End M:*


        public void ListInventory(ConvertedLists cvlLists) {
            
            Vehicle[] vList = cvlLists.VList;
            Inventory[] iList = cvlLists.IList;

            //Recall: id,vehicleid,numonhand,price,cost,
            for (int i = 0; i < vList.Length; i++)
            {
                Console.WriteLine(
                                    "Make: " +
                                    vList[iList[i].VehicleId - 1].Make +
                                    ", Model: " +
                                    vList[iList[i].VehicleId - 1].Model +
                                    ", Quantity On Hand: " +
                                    iList[i].NumOnHand +
                                    ", Price: " +
                                    iList[i].Price +
                                    ", " + 
                                    "Cost " +
                                    iList[i].Cost
                                   );
            }//End F:*

        }//End M:*

        public void AddInventoryItem(ConvertedLists cvlLists)
        {

            //Recall: id,vehicleid,numonhand,price,cost,
            try
            {
                //Declare-Define: get needed lists for program clarity.
                Vehicle[] vList = cvlLists.VList;
                Inventory[] iList = cvlLists.IList;

                //Get: items from user to create appropriate objs
                Console.WriteLine("You selected Add Inventory Item\n" +
                    "What is the make of the vehicle you want to add to inventory? Expected input [a-z].");
                string uMake = Console.ReadLine();

                Console.WriteLine("What is the model of the vehicle you want to add to inventory? Expected input [a-z].");
                string uModel = Console.ReadLine();

                Console.WriteLine("What is the year of the vehicle you want to add to inventory? Expected input [0-9].");
                int uYear = int.Parse(Console.ReadLine());

                Console.WriteLine("What is the quantity of the vehicle you want to add to inventory? Expected input [0-9].");
                int uQuantity = int.Parse(Console.ReadLine());

                Console.WriteLine("What is the retail price of the vehicle you want to add to inventory? Expected input [0-9].");
                double uPrice = double.Parse(Console.ReadLine());

                Console.WriteLine("What is the pruchase price of the vehicle you want to add to inventory? Expected input [0-9].");
                double uCost = double.Parse(Console.ReadLine());

                Console.WriteLine("What is the condition of the vehicle you want to add to inventory? Expected input [a-z] new/used binary.");
                string uCond = Console.ReadLine();

                //Recall: id,make,model,year,condition,
                long lastId = vList[vList.Length - 1].Id;

                //Build: new vehicle obj with user data.
                Vehicle newV = new Vehicle(lastId + 1, uMake, uModel, uYear, uCond);
                Vehicle[] newVList = new Vehicle[vList.Length + 1];

                //Transfer: items to a list with more room.
                for (int i = 0; i < vList.Length; i++) {
                    newVList[i] = vList[i];
                }//End F:*

                newVList[newVList.Length - 1] = newV;

                //Update: master list holder with modified, expanded lists.
                cvlLists.VList = newVList;

                long lastInventId = iList[iList.Length - 1].Id;

                //Build: inventory obj with user data
                Inventory newI = new Inventory(lastInventId + 1, newV.Id, uQuantity, uPrice, uCost);
                Inventory[] newIList = new Inventory[iList.Length + 1];

                //Transfer: items to a list with more room.
                for (int i = 0; i < iList.Length; i++) {
                    newIList[i] = iList[i];
                }//End F:*

                newIList[newIList.Length - 1] = newI;

                //Update: master list holder with modified, expanded lists.
                cvlLists.IList = newIList;

            }//End TRY:*

            catch (Exception ex){
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

        }//End M:*

        public void FindInventoryItem(ConvertedLists cvlLists)
        {
            try {
                
                Inventory[] iList = cvlLists.IList;
                Vehicle[] vList = cvlLists.VList;

                Console.WriteLine(
                    "You selected Find Inventory Item\n" +
                    "What is the make of th vehicle you wish to find? Expected input [a-z].");
                    string uMake = Console.ReadLine();

                Console.WriteLine("What is the model of the vehicle you wish to find? Expected input [a-z].");
                string uModel = Console.ReadLine();

                Console.WriteLine("What is the year of the vehicle you wish to find? Expected input [0-9].");
                int uYear = int.Parse(Console.ReadLine());

                for (int i = 0; i < iList.Length; i++) {

                    if (vList[i].Make == uMake && vList[i].Model == uModel && vList[i].Year == uYear) {
                        Console.WriteLine(
                            "Make: " + 
                            vList[i].Make + 
                            ", Model: " + 
                            vList[i].Model +
                            ", Year: " + 
                            vList[i].Year + 
                            ", Quantity On Hand: " + 
                            iList[i].NumOnHand + 
                            ", Price: " + 
                            iList[i].Price +
                            ", Cost: " +
                            iList[i].Cost);
                    }//End I:*

                }//End F:*

            }//End TRY:*

            catch (Exception ex) {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

        }//End M:*

        public void DeleteInventoryItem(ConvertedLists cvlLists)
        {
            try {

                Inventory[] iList = cvlLists.IList;
                Vehicle[] vList = cvlLists.VList;

                Console.WriteLine("You selected Delete Inventory Item\n" +
                    "What is the make of the vehicle your looking to delete? Expecting input [a-z]");
                string uMake = Console.ReadLine();

                Console.WriteLine("What is the model of the vehicle your looking to delete? Expecting input [a-z]");
                string uModel = Console.ReadLine();

                Console.WriteLine("What is the year of the vehicle your looking to delete? Expecting input [0-9]");
                int uYear = int.Parse(Console.ReadLine());

                Vehicle[] newVList = new Vehicle[vList.Length - 1];
                Inventory[] newIList = new Inventory[iList.Length - 1];

                for (int i = 0; i < vList.Length; i++) {
                    
                    if (vList[i].Make == uMake && vList[i].Model == uModel && vList[i].Year == uYear) {
                        
                        for (int j = 0; j < i; j++) {
                            newVList[j] = vList[j];
                        }//End F:*           

                        int counter = i + 1;
                        for (int j = i; j < newVList.Length; j++) {
                            newVList[j] = vList[counter];
                            newVList[j].Id = newVList[j].Id - 1;
                            counter++;
                        }//End F:*

                        cvlLists.VList = newVList;

                        for (int j = 0; j < i; j++) {
                            newIList[j] = iList[j];
                        }//End F:*

                        counter = i + 1;
                        for (int j = i; j < newIList.Length; j++) {
                            newIList[j] = iList[counter];
                            counter++;
                        }//End F:*

                        cvlLists.IList = newIList;

                    }//End I:*

                }//End F:*

            }//End TRY:*

            catch (Exception ex) {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*
        }//End M:*

        public int RepairsMenu()
        {
            int uChoice = 0;
            
            try {
                Console.WriteLine(
                "You selected Modify Repairs\n" +
                "Menu options range from 1-5 and expect an appropriate integer as an input response\n" +
                "1: List Repairs, 2: Add Repair Item, 3: Find Repair Item, 4: Delete Repair Item, 5: Return Previous Menu");
                uChoice = int.Parse(Console.ReadLine());
                return uChoice;
            }//End TRY:*

            catch (Exception ex)
            {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

            return uChoice;
        }//End M:*

        public void ListRepairs(ConvertedLists cvlLists)
        {

            Repair[] rList = cvlLists.RList;
            Vehicle[] vList = cvlLists.VList;
            Inventory[] iList = cvlLists.IList;

            //Recall: id,inventoryid,whattorepair,
            for (int i = 0; i < rList.Length; i++) {
                Console.WriteLine(
                    vList[i].Make + 
                    ", " +
                    vList[i].Model +
                    ", " + 
                    vList[i].Year +
                    ", " + 
                    rList[i].WhatTo);   
            }//End F:*

        }//End M:*

        public void AddRepairItem(ConvertedLists cvlLists) {
            
            try
            {
                Repair[] rList = cvlLists.RList;
                Vehicle[] vList = cvlLists.VList;
                Inventory[] iList = cvlLists.IList;

                Console.WriteLine("You selected Add Repair Item\n" +
                    "What is the make of the vehicle you want to apply the new repair item to? Expecting input [a-z]");
                string uMake = Console.ReadLine();

                Console.WriteLine(
                    "What is the model of the vehicle you want to apply the new repair item to? Expecting input [a-z]");
                string uModel = Console.ReadLine();

                Console.WriteLine(
                    "What is the year of the vehicle you want to apply the new repair item to? Expecting input [0-9]");
                int uYear = int.Parse(Console.ReadLine());

                Console.WriteLine(
                    "What is the new repair item you want to create for the vehicle you specified? Expecting input [a-z]");
                string uRepair = Console.ReadLine();

                //Recall: id,inventoryid,whattorepair,

                Repair[] newRList = new Repair[rList.Length + 1];
                long lastRId = rList[rList.Length - 1].Id;

                Boolean flag = false;
                
                for (int i = 0; i < vList.Length; i++) {
                    
                    if (vList[i].Make == uMake && vList[i].Model == uModel && vList[i].Year == uYear)
                    {
                        Repair newR = new Repair(lastRId + 1, iList[i].Id, uRepair);

                        for (int j = 0; j < rList.Length; j++)
                        {
                            newRList[j] = rList[j];
                        }//End F:*

                        newRList[newRList.Length - 1] = newR;

                        cvlLists.RList = newRList;

                        flag = true; 

                    }//End I:*

                }//End F:*

                if (!flag) {
                    Console.WriteLine(
                           "What is the condition of the vehicle you want to apply the repair to? Expected input [a-z] new/used binary.");
                    string uCond = Console.ReadLine();

                    Console.WriteLine(
                        "What is the Quantity of the vehicle you want to apply the repair to? Expected input [0-9].");
                    int uQuantity = int.Parse(Console.ReadLine());

                    Console.WriteLine(
                        "What is the retail price of the vehicle you want to apply the repair to? Expected input [0-9].");
                    double uPrice = double.Parse(Console.ReadLine());

                    Console.WriteLine(
                        "What is the cost of the vehicle you want to apply the repair to? Expected input [0-9].");
                    double uCost = double.Parse(Console.ReadLine());

                    //Recall: id,make,model,year,condition,
                    //Recall: id,vehicleid,numonhand,price,cost,

                    Vehicle newV = new Vehicle(
                        vList[vList.Length - 1].Id + 1,
                        uMake,
                        uModel,
                        uYear,
                        uCond);

                    Vehicle[] newVList = new Vehicle[vList.Length + 1];

                    for (int j = 0; j < vList.Length; j++)
                    {
                        newVList[j] = vList[j];
                    }//End F:*

                    newVList[newVList.Length - 1] = newV;

                    cvlLists.VList = newVList;

                    Inventory newI = new Inventory(
                        iList[iList.Length - 1].Id + 1,
                        newV.Id,
                        uQuantity,
                        uPrice,
                        uCost);

                    Inventory[] newIList = new Inventory[iList.Length + 1];

                    for (int j = 0; j < iList.Length; j++)
                    {
                        newIList[j] = iList[j];
                    }//End F:*

                    newIList[newIList.Length - 1] = newI;

                    cvlLists.IList = newIList;

                    Repair newR = new Repair(lastRId + 1, newIList[newIList.Length - 1].Id + 1, uRepair);

                    for (int j = 0; j < rList.Length; j++)
                    {
                        newRList[j] = rList[j];
                    }//End F:*

                    newRList[newRList.Length - 1] = newR;

                    cvlLists.RList = newRList;

                }//End I:*

            }//End TRY:*

            catch (Exception ex)
            {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

        }//End M:*

        public void FindRepairItem(ConvertedLists cvlLists) {
            
            try
            {
                Repair[] rList = cvlLists.RList;
                Vehicle[] vList = cvlLists.VList;
                Inventory[] iList = cvlLists.IList;


                Console.WriteLine("You selected Find Repair Item\n" +
                    "What is the make of the vehicle you want to find? Expecting input [a-z]");
                string uMake = Console.ReadLine();

                Console.WriteLine(
                    "What is the model of the vehicle you want to find? Expecting input [a-z]");
                string uModel = Console.ReadLine();

                Console.WriteLine(
                    "What is the year of the vehicle you want to find? Expecting input [0-9]");
                int uYear = int.Parse(Console.ReadLine());


                for (int i = 0; i < vList.Length; i++) {
                    
                    if (vList[i].Make == uMake && vList[i].Model == uModel && vList[i].Year == uYear) {

                        long tempId = vList[i].Id;

                        for (int j = 0; j < rList.Length; j++) {
                            
                            if (rList[j].InventId == tempId) {
                                Console.WriteLine(
                            "Make: " +
                            vList[i].Make +
                            ", Model: " +
                            vList[i].Model +
                            ", Year: " +
                            vList[i].Year +
                            ", Inventory Id: " +
                            iList[i].Id +
                            ", Repair: " +
                            rList[j].WhatTo);

                            }//End I:*

                        }//End F:*
                       
                    }//End I:*

                }//End F:*

            }//End TRY:*
            catch (Exception ex)
            {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*
        }//End M:*

        public void DeleteRepairItem(ConvertedLists cvlLists) {
            
            try
            {
                Repair[] rList = cvlLists.RList;

                Console.WriteLine("You selected Delete Repair Item\n" +
                    "What is the repair item you want to delete? Expected input [a-z]");
                string uRepair = Console.ReadLine();

                Repair[] newRList = new Repair[rList.Length - 1];

                for (int i = 0; i < rList.Length; i++) {

                    if (rList[i].WhatTo == uRepair) {

                        for(int j = 0; j < i; j++) {
                            newRList[j] = rList[j];
                        }//End F:*

                        int counter = i + 1;
                        for (int j = i; j < newRList.Length; j++) {
                            newRList[j] = rList[counter];
                            newRList[j].Id = newRList[j].Id - 1;
                            counter++;
                        }//End F:*

                        cvlLists.RList = newRList;

                    }//End I:*

                }//End F:*

            }//End TRY:*

            catch (Exception ex)
            {
                Console.WriteLine("Number format exception " + ex.Message);
            }//End CAT:*

        }//End M:*

        public void StartMenu(ConvertedLists clTest, string fV, string fI, string fR) {
            
            FileIO data = new FileIO();

            clTest = data.FormatData(fV, fI, fR);

            Menu menu = new Menu();

    
            Boolean flag = true;

            while (flag)
            {

                int uChoice = menu.MainMenu();

                if (uChoice == 1)
                {
                    uChoice = menu.VehicleMenu();
                    
                    if (uChoice == 1) {
                        menu.ListVehicles(clTest);
                    }//End I:*

                    else if (uChoice == 2) {
                        menu.AddVehicle(clTest);
                    }//End EI:*

                    else if (uChoice == 3) {
                        menu.FindVehicle(clTest);
                    }//End EI:*

                    else if (uChoice == 4) {
                        menu.DeleteVehicle(clTest);
                    }//End EI:*

                    else if (uChoice == 5) {
                        StartMenu(clTest, fV, fI, fR);
                    }//End EI:*

                }//End I:*

                else if (uChoice == 2)
                {
                    uChoice = menu.InventoryMenu();

                    if (uChoice == 1) {
                        menu.ListInventory(clTest);
                    }//End I:*

                    else if (uChoice == 2) {
                        menu.AddInventoryItem(clTest);
                    }//End EI:*

                    else if (uChoice == 3) {
                        menu.FindInventoryItem(clTest);
                    }//End EI:*

                    else if (uChoice == 4) {
                        menu.DeleteInventoryItem(clTest);
                    }//End EI:*

                    else if (uChoice == 5) {
                        StartMenu(clTest, fV, fI, fR);
                    }//End EI:*

                }//End EI:*

                else if (uChoice == 3)
                {
                    uChoice = menu.RepairsMenu();

                    if (uChoice == 1) {
                        menu.ListRepairs(clTest);
                    }//End I:*
                    
                    else if (uChoice == 2)
                    {
                        menu.AddRepairItem(clTest);
                    }//End I:*
                    
                    else if (uChoice == 3)
                    {
                        menu.FindRepairItem(clTest);
                    }//End I:*
                    
                    else if (uChoice == 4)
                    {
                        menu.DeleteRepairItem(clTest);
                    }//End I:*

                    else if (uChoice == 5)
                    {
                        StartMenu(clTest, fV, fI, fR);
                    }//End I:*

                }//End EI:*

                else if (uChoice == 4)
                {
                    data.SaveAll(clTest, fV, fI, fR);       
                    flag = false;
                }//End EI:*

            }//End W:*

        }//End M:*

    }//End CL:*

   

}//End NS:*
