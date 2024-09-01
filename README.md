using System;
using System.Collections.Generic;

namespace Project1
{
    public class DeliveryOrder : Order
    {
        public string Address { get; set; }
        private const int DeliveryCharge = 2000; // in pence
        private const int FreeDeliveryThreshold = 20000; // in pence

        public override void OutputOrder()
        {
            if (string.IsNullOrWhiteSpace(Address))
            {
                throw new Exception("Delivery address cannot be empty.");
            }

            base.OutputOrder();
            int total = CalculateTotal();
            if (total < FreeDeliveryThreshold)
            {
                total += DeliveryCharge;
                Console.WriteLine($"Delivery charge: {DeliveryCharge / 100.0:C}");
            }
            else
            {
                Console.WriteLine("Free delivery!");
            }
            Console.WriteLine($"Final Total: {total / 100.0:C}");
        }
    }
}