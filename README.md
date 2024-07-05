# Geolocater 
This Is a Geolocator with City/Region/Postal/Location/Org/Time zone/Including A Google Maps Link to the Coordinates Of The Location.

Here is the code:Copy it or download and insert in to visual studios watch Tut on my youtube: https://www.youtube.com/channel/UC1WogEsFOEr6ytEAa2vb1BA
---------------------------------------------------------------------------------------------
         ⬇️
         ⬇️
         ⬇️
        






using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Net.Http;
using Newtonsoft.Json;
using System.Runtime;

namespace geolocate
{

    public class Data
    {
        public string City { get; set; }
        public string Region { get; set; }
        public string Country { get; set; }
        public string Loc { get; set; }
        public string Org { get; set; }
        public string Postal { get; set; }
        public string Timezone { get; set; }
    }
    internal class Program
    {
        static async Task Main(string[] args)
        {
            Console.Title = "Geolocator";
            Console.Write("Enter IP Address: ");
            string ip = Console.ReadLine();
            string url = $"https://ipinfo.io/{ip}/json";
            using (HttpClient client = new HttpClient())
            {
                try
                {
                    HttpResponseMessage  httpResponseMessage = await client.GetAsync(url);
                    httpResponseMessage.EnsureSuccessStatusCode();

                    Console.WriteLine("[+]Request Successfully Made");

                    string responseData = await httpResponseMessage.Content.ReadAsStringAsync();
                    Data ipinfo = JsonConvert.DeserializeObject<Data>(responseData);

                    Console.Clear();
                    Console.WriteLine($"Country: {ipinfo.Country}");
                    Console.WriteLine($"City: {ipinfo.City}");
                    Console.WriteLine($"Coordinates: {ipinfo.Loc}");
                    Console.WriteLine($"Postal Code: {ipinfo.Postal}");
                    Console.WriteLine($"Region: {ipinfo.Region}");
                    Console.WriteLine($"ASN: {ipinfo.Org}");
                    string[] Coord =ipinfo.Loc.Split(',');
                    Console.WriteLine($"Google Maps:https://www.google.com/maps/?q={Coord[0]},{Coord[1]}");
                }   
                catch (HttpRequestException ex)
                { 
                    Console.WriteLine($"Error: {ex. Message}");
                }           
            }   
        }
    }
}
