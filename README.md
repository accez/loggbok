# loggbok
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace LoggBoken
{
    class Program
    {
    
        static void DisplayMeny()
        {
            DateTime dateTime = DateTime.Now;

            //Meny text
            Console.WriteLine("\t" + dateTime);
            Console.WriteLine("\n \t Loggboken!");
            Console.WriteLine("\t [1] Skriv nytt inlägg i loggboken");
            Console.WriteLine("\t [2] Skriv ut alla loggar");
            Console.WriteLine("\t [3] Sök inlägg i loggboken");
            Console.WriteLine("\t [4] Avsluta");
            Console.Write("\t Välj:");
        }

        static void Main(string[] args)
        {
            List<string[]> loggBoken = new List<string[]> { };
            string[] inlägg = new string[3]; // Vektor med 3 index
            DateTime dateTime = DateTime.Now;
            bool kör = true;
            while (kör)
            {
                DisplayMeny();

                int val;
                int.TryParse(Console.ReadLine(), out val); //tryparse funktion för menyvalet

                //Switch funktion för meny val 
                switch (val)
                {
                    case 1:
                        Console.Clear();
                        inlägg = new string[3]; //skappar ett nytt inlägg i loggboken
                        
                        //Får skriva in titel till array
                        Console.Write("Skriv titel: ");
                        inlägg[0] = Console.ReadLine();
                        Console.Clear();
                        
                        //Skriver inlägget till array
                        Console.Write("Skriv in inlägg: ");
                        inlägg[1] = Console.ReadLine();
                        Console.Clear();

                        //lägger till datum och tid i loggen adderar det till arreyen
                        var tidFörInlägg = Convert.ToString(dateTime);
                        inlägg[2] = tidFörInlägg;
                        Console.Clear();

                        //adderar allt information samlad till listan
                        loggBoken.Add(inlägg);
                        Console.Clear();
                        break;
                    case 2:
                        Console.Clear();
                        Console.WriteLine("Det du har sparat i loggboken är: ");
                        foreach (string[] item in loggBoken) //for each som skriver ut alla titlar,loggtexter och tid och datum som är sparat i "loggBoken"
                        {
                            Console.WriteLine("\t Titel: {0}" + "\n \t {1}" + "\n \t {2}"
                                ,item[0],item[1],item[2] );
                             }
                        break;
                    case 3: //Sökfunktion
                        Console.Clear();
                        Console.Write("Sök efter titel på loggar: ");
                        string sök = Console.ReadLine();

                        foreach (string[] text in loggBoken) // foreach som söker efter arrayen i loggboken
                        {
                            if (text[0].Contains(sök)) //Om arrayen hittas i Console.Readline så skrivs den ut. Använder in if sats för det
                            {
                                Console.WriteLine("\n" + text[0] + "\n" + text[1] + "\n" + text[2]); 
                            }
                           else //Om "sök" inte hittar något
                            {
                                Console.WriteLine("Sökning misslyckades");
                            }
                        }
                            break;
                    case 4:
                        //Avslutar programmet
                        Console.Clear();
                        Console.WriteLine("Avslutar loggboken!");
                        kör = false; //kör blir false och programmet stängs ner
                        break;

                    default:
                        Console.WriteLine("Välj riktigt menyval!"); // Om du skriver in något annat en menyvalen
                        break;
                }
                Console.ReadLine();
            }
        }
    }
}
