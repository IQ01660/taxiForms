# taxiForms
``` C#
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace taxiProblemForms
{
    public partial class Form1 : Form
    {
        
        public Form1()
        {
            InitializeComponent();
        }

        public void Form1_Load(object sender, EventArgs e)
        {
            this.comboBoxCust = new System.Windows.Forms.ComboBox();
            this.comboBoxCust.FormattingEnabled = true;
            this.comboBoxCust.Location = new System.Drawing.Point(366, 210);
            this.comboBoxCust.Name = "comboBoxCust";
            this.comboBoxCust.Size = new System.Drawing.Size(140, 21);
            this.comboBoxCust.TabIndex = 17;
            this.Controls.Add(this.comboBoxCust);
            this.comboBoxCust.Click += new System.EventHandler(this.comboBoxCust_Select);


            // creating default customers 
            Customer ikram = new Customer("Ikram", 0, 0);
            Customer james = new Customer("James", 10, 10);
            // allocating the customers to the list
            foreach (var item in CustomerHolder.customerList)
            {
                this.comboBoxCust.Items.Add(item.Name);
            }
            //creating default taxis

        }
        private void comboBoxCust_Select(object boxObj , EventArgs eve)
        {
            ComboBox mybox = boxObj as ComboBox;
            MessageBox.Show(mybox.SelectedItem);
             
        }

        private void addCustomerBtn_Click(object sender, EventArgs e)
        {
            // adding new customers with add button
            string newName = custName.Text;
            int newXCust = Convert.ToInt32(xCust.Text);
            int newYCust = Convert.ToInt32(yCust.Text);
            CustomerHolder.customerList.Add(new Customer(newName, newXCust, newYCust));
            this.comboBoxCust.Items.Add(newName);
        }

        private void addTaxiBtn_Click(object sender, EventArgs e)
        {

        }
    }
    class SelectedCustomerHolder
    {
        List<Customer> selCust = new List<Custsomer>();
    }
    class TaxiHolder
    {
        static public List<Taxi> taxiList = new List<Taxi>();
    }
    class CustomerHolder
    {
        // list to hold all customers
        static public List<Customer> customerList = new List<Customer>();
    }

    class Taxi
    {
        public string TaxiNum;
        public double Distance;
        public double Price;
        public int xTaxi;
        public int yTaxi;
        public Taxi(string _taxiNum, int _xtaxi , int _ytaxi)
        {
            this.TaxiNum = _taxiNum;
            this.xTaxi = _xtaxi;
            this.yTaxi = _ytaxi;
            //this.Distance = this.calculateDistance();
            this.Price = this.Distance * 3 / 10;
        }
        
        private double calculateDistance(Customer _customer)
        {
            return Math.Floor(Math.Sqrt(((this.xTaxi - _customer.xCust) * (this.xTaxi - _customer.xCust)) + ((this.yTaxi - _customer.yCust) * (this.yTaxi - _customer.yCust))));
        }
    }
    class Customer
    {
        public string Name;
        public int xCust;
        public int yCust;
        public Customer(string _name, int _xcust , int _ycust)
        {
            this.Name = _name;
            this.xCust = _xcust;
            this.yCust = _ycust;
            CustomerHolder.customerList.Add(this);
        }
    }
}
```
