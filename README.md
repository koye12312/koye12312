using System;
using System.Collections.Generic;

namespace Project1
{
    public class Pizza : FoodItem
    {
        public List<Topping> Toppings { get; set; } = new List<Topping>();

        public Pizza(string name, List<Topping> toppings, int price)
        {
            Name = name;
            Toppings = toppings;
            Price = price;
        }

        public void RemoveTopping(string toppingName)
        {
            Toppings.RemoveAll(t => t.Name.Equals(toppingName, StringComparison.OrdinalIgnoreCase));
        }

        public void AddTopping(Topping topping)
        {
            Toppings.Add(topping);
            Price += topping.Price;  // Add the price of the new topping to the pizza price
        }

        public override void PrintDetails()
        {
            Console.WriteLine($"Pizza: {Name}, Price: {Price}");
            Console.Write("Toppings: ");
            foreach (var topping in Toppings)
            {
                Console.Write($"{topping.Name} ");
            }
            Console.WriteLine();
        }
    }
}