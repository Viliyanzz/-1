using System;
using System.Collections.Generic;

// Bazov klas za geroi
public class Geroi
{
    // Svoystva na geroia
    public string Ime { get; set; }
    public int Zdrave { get; set; }
    public int Mana { get; set; }
    public List<Magiya> Magii { get; set; }

    // Konstruktur za suzdavane na nov geroi
    public Geroi(string ime, int zdrave, int mana)
    {
        Ime = ime;
        Zdrave = zdrave;
        Mana = mana;
        Magii = new List<Magiya>();
    }

    // Metod za izpulnenie na magiya
    public string IzpulniMagiya(string imeNaMagiya)
    {
        // Namirane na magiyata po ime
        Magiya magiya = Magii.Find(m => m.Ime == imeNaMagiya);
        if (magiya != null)
        {
            // Proverka dali geroiat ima dostatachno mana
            if (Mana >= magiya.ManaCena)
            {
                Mana -= magiya.ManaCena;
                return magiya.Efekt;
            }
            else
            {
                return $"{Ime} nyama dostatachno mana, za da izpolzva {magiya.Ime}.";
            }
        }
        else
        {
            return $"{Ime} ne znae magiyata {imeNaMagiya}.";
        }
    }

    // Metod za nauchavane na nova magiya
    public void NauchiNovaMagiya(Magiya magiya)
    {
        Magii.Add(magiya);
        Console.WriteLine($"{Ime} nauchi magiyata {magiya.Ime}.");
    }
}

// Klas za magiya
public class Magiya
{
    public string Ime { get; set; }
    public int ManaCena { get; set; }
    public string Efekt { get; set; }

    // Konstruktur za suzdavane na nova magiya
    public Magiya(string ime, int manaCena, string efekt)
    {
        Ime = ime;
        ManaCena = manaCena;
        Efekt = efekt;
    }
}

// Klas za voin, nasledyavasht ot Geroi
public class Voin : Geroi
{
    public Voin(string ime) : base(ime, 150, 50)
    {
        NauchiNovaMagiya(new Magiya("Udar", 10, "Moshten udar s mele ataka."));
        NauchiNovaMagiya(new Magiya("Shtit Udar", 15, "Zashtemetiyavasht udar s shtit."));
    }
}

// Klas za magyosnik, nasledyavasht ot Geroi
public class Magyosnik : Geroi
{
    public Magyosnik(string ime) : base(ime, 100, 200)
    {
        NauchiNovaMagiya(new Magiya("Ogneno kulbo", 20, "Ognena eksplozia, koyato nanasya shteti."));
        NauchiNovaMagiya(new Magiya("Lechenie", 15, "Vuzstanovyava zdrave."));
    }
}

public class Programa
{
    public static void Main()
    {
        // Suzdavame voin i magyosnik
        Voin voin = new Voin("Gosho");
        Magyosnik magyosnik = new Magyosnik("Pesho");

        // Demonstratsia na magiite na voina
        Console.WriteLine(voin.IzpulniMagiya("Udar"));
        Console.WriteLine(voin.IzpulniMagiya("Shtit Udar"));
        Console.WriteLine(voin.IzpulniMagiya("Neizvestna Magiya"));

        // Demonstratsia na magiite na magyosnika
        Console.WriteLine(magyosnik.IzpulniMagiya("Ogneno kulbo"));
        Console.WriteLine(magyosnik.IzpulniMagiya("Lechenie"));
        Console.WriteLine(magyosnik.IzpulniMagiya("Neizvestna Magiya"));
    }
}
