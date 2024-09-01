using System;
using System.Collections.Generic;

namespace Project1
{
    public class Burger : FoodItem
    {
        public List<Garnish> Garnishes { get; set; } = new List<Garnish>();

        public Burger(string name, List<Garnish> garnishes, int price)
        {
            Name = name;
            Garnishes = garnishes;
            Price = price;
        }

        public void RemoveGarnish(string garnishName)
        {
            Garnishes.RemoveAll(g => g.Name.Equals(garnishName, StringComparison.OrdinalIgnoreCase));
        }

        public void AddGarnish(Garnish garnish)
        {
            Garnishes.Add(garnish);
            Price += garnish.Price;  // Add the price of the new garnish to the burger price
        }

        public override void PrintDetails()
        {
            Console.WriteLine($"Burger: {Name}, Price: {Price}");
            Console.Write("Garnishes: ");
            foreach (var garnish in Garnishes)
            {
                Console.Write($"{garnish.Name} ");
            }
            Console.WriteLine();
        }
    }
}