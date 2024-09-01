using System;
using System.Collections.Generic;

namespace Project1
{
    public class Order
    {
        public string CustomerName { get; set; }
        public List<FoodItem> Items { get; set; } = new List<FoodItem>();

        public virtual void OutputOrder()
        {
            Console.WriteLine($"Order for {CustomerName}:");
            foreach (var item in Items)
            {
                item.PrintDetails();
            }

            int total = CalculateTotal();
            Console.WriteLine($"Total: {total / 100.0:C}");
        }

        public int CalculateTotal()
        {
            int total = 0;
            foreach (var item in Items)
            {
                total += item.Price;
            }
            return total;
        }
    }
}