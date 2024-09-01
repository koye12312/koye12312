using System;
using System.Collections.Generic;

namespace Project1
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Loading menu...");
            TakeawayShop.LoadMenu("menu.txt");

            Console.WriteLine("Welcome to the Takeaway Shop!");
            Console.Write("Please enter your name: ");
            string customerName = Console.ReadLine();

            Console.Write("Is this a delivery order? (yes/no): ");
            string deliveryResponse = Console.ReadLine().ToLower();

            Order order;
            if (deliveryResponse == "yes")
            {
                Console.Write("Please enter your address: ");
                string address = Console.ReadLine();
                order = new DeliveryOrder
                {
                    CustomerName = customerName,
                    Address = address
                };
            }
            else
            {
                order = new Order
                {
                    CustomerName = customerName
                };
            }

            Console.WriteLine("\nHere is the menu:");
            DisplayMenu();

            bool addingItems = true;
            while (addingItems)
            {
                Console.Write("\nEnter the name of the food item you want to order (or type 'done' to finish): ");
                string itemName = Console.ReadLine();

                if (itemName.ToLower() == "done")
                {
                    addingItems = false;
                }
                else
                {
                    var item = TakeawayShop.Menu.Find(f => f.Name.Equals(itemName, StringComparison.OrdinalIgnoreCase));
                    if (item != null)
                    {
                        CustomizeItem(item);
                        order.Items.Add(item);
                        Console.WriteLine($"{itemName} added to your order.");
                    }
                    else
                    {
                        Console.WriteLine("Sorry, that item is not on the menu.");
                    }
                }
            }

            if (order.Items.Count > 0)
            {
                Console.WriteLine("\nProcessing your order...");
                order.OutputOrder();
            }
            else
            {
                Console.WriteLine("You did not order anything.");
            }
        }

        static void CustomizeItem(FoodItem item)
        {
            if (item is Pizza pizza)
            {
                Console.Write("Do you want to remove any toppings? (yes/no): ");
                if (Console.ReadLine().ToLower() == "yes")
                {
                    Console.WriteLine("Enter the topping(s) you want to remove (comma separated): ");
                    string[] toppingsToRemove = Console.ReadLine().Split(',');

                    foreach (var topping in toppingsToRemove)
                    {
                        pizza.RemoveTopping(topping.Trim());
                    }
                }

                Console.Write("Do you want to add any extra toppings? (yes/no): ");
                if (Console.ReadLine().ToLower() == "yes")
                {
                    Console.WriteLine("Enter the topping(s) you want to add (comma separated): ");
                    string[] extraToppings = Console.ReadLine().Split(',');

                    foreach (var toppingName in extraToppings)
                    {
                        var topping = new Topping { Name = toppingName.Trim(), Price = 100 }; // Example price
                        pizza.AddTopping(topping);
                    }
                }
            }
            else if (item is Burger burger)
            {
                Console.Write("Do you want to remove any garnishes? (yes/no): ");
                if (Console.ReadLine().ToLower() == "yes")
                {
                    Console.WriteLine("Enter the garnish(es) you want to remove (comma separated): ");
                    string[] garnishesToRemove = Console.ReadLine().Split(',');

                    foreach (var garnish in garnishesToRemove)
                    {
                        burger.RemoveGarnish(garnish.Trim());
                    }
                }

                Console.Write("Do you want to add any extra garnishes? (yes/no): ");
                if (Console.ReadLine().ToLower() == "yes")
                {
                    Console.WriteLine("Enter the garnish(es) you want to add (comma separated): ");
                    string[] extraGarnishes = Console.ReadLine().Split(',');

                    foreach (var garnishName in extraGarnishes)
                    {
                        var garnish = new Garnish { Name = garnishName.Trim(), Price = 50 }; // Example price
                        burger.AddGarnish(garnish);
                    }
                }
            }
        }

        static void DisplayMenu()
        {
            foreach (var item in TakeawayShop.Menu)
            {
                item.PrintDetails();
            }
        }
    }
}