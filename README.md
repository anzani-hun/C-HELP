# CSV fájlban, ha van fejléc akkor:

`sr.ReadLine();`

---


# megszámlálás:

```ruby
int[] tomb = new int[] {1, 2, 3, 4, 5, 6};
            int db = 0;
            for (int i = 0; i < tomb.Length; i++)
            {
                if (tomb[i] > 5)
                {
                    darab++;
                }
            }
            Console.WriteLine($"A tömb elemei között: {darab} db 5-nál nagyobb szám van!");
```
```ruby
osztályból:
static List<Epulet> epuletLista = new List<Epulet>();
Console.WriteLine($"Az összes beolvasott épületek száma: {epuletLista.Count}!");

```


---


# összegzés:

```ruby
 int[] tomb = new int[] {1, 2, 3, 4, 5, 6, 7, 8};
            int osszeg = 0;
            for (int i = 0; i < tomb.Length; i++)
            {
                osszeg = osszeg + tomb[i];
            }
            Console.WriteLine($"A tömb elemeinek értékének az összege: {osszeg}");
```


---


# MIN és MAX kiválasztása:

```ruby
            int[] tombLista = new int[] { 1, 10, 30, 50, 60, 55 };
            int min = tombLista[0];
            int max = tombLista[0];

            for (int i = 0; i < tombLista.Length; i++)
            {
                if (tombLista[i] > max)
                {
                    max = tombLista[i];
                }
            }
            Console.WriteLine($"A legnagyobb szám: {max}");
            Console.WriteLine($"A legkisebb szám: {min}");
```


---






# STREAMWRITER használata TXT írásra:

```ruby
string fajlneve = "adatok.txt";

StreamWriter iras = new StreamWriter(fajlneve, false, Encoding.Default);

double r = 23.4;
iras.WriteLine("Programozó = ÉN");
iras.WriteLine("PI = {0}", Math.PI);
iras.WriteLine("sugár = {0}", r);
iras.WriteLine("Kerület = {0}", 2 * r * Math.PI);

iras.Close();
```

---

# STREAMREADER használata TXT olvasásra:

```ruby
  using (StreamReader olvaso = new StreamReader("adatok.txt", Encoding.UTF8))
  {
      //ha van fejléc a csv fájlban, akkor azt ki kell hagyni:
      //olvaso.ReadLine();


      //amíg a végére nem ér, addig olvassa be az új sorokat
      while (!olvaso.EndOfStream)
      {
          string[] sor = olvaso.ReadLine().Split(';').Trim('"');


          //string vezeteknev, string keresztnev, int eletKor, int fizetes, string beosztas
          Proba proba = new Proba(sor[0], sor[1], int.Parse(sor[2]), int.Parse(sor[3]), sor[4]);

          probaLista.Add(proba);
      }

  }
```

---
---

# KEREKÍTÉS

```ruby
            double ertek = 123.456789;
            double kerekitettErtek = Math.Round(ertek, 2); // Két tizedesjegyre kerekít
            Console.WriteLine(kerekitettErtek); // Kiírja: 123.46
```
---


# egy listából: SUM, AVG, MIN, MAX, FIRST, LAST

```ruby
            double atlagFizetes = probaLista.Average(p => p.Fizetes);
            atlagFizetes = Math.Round(atlagFizetes, 2);

            Console.WriteLine($"\nAz összes fizetés átlaga: {atlagFizetes} ");
```

```ruby
            //összes SEGÉD-et ki kell iratni névvel egy listából:
            foreach (Proba adat in probaLista)
            {
                if (adat.Beosztas.Contains("seged"))
                {
                    Console.WriteLine($"{adat.Keresztnev} {adat.Beosztas}");
                }
            }
```


```ruby
            //az összes életkor ÖSSZEGE:
            int osszesKor = probaLista.Sum(p => p.EletKor);

            Console.WriteLine($"Az összes életkor összege: {osszesKor} év.");
```


```ruby
            //egy listából a legnagyobb szám kiíratása: legidősebb ember megtalálása életkor alapján
            int maxKor = probaLista.Max(p => p.EletKor);
            Proba legidosebb = probaLista.FirstOrDefault(p => p.EletKor == maxKor);

            if (legidosebb != null)
            {
                Console.WriteLine($"A legidősebb ember: {legidosebb.Keresztnev}, kora: {legidosebb.EletKor} év.");
            }
```


```ruby
            //első és utolsó név kiiratása a listából:
                // Kiírjuk az első elem keresztnevét
                Console.WriteLine($"\nElső ember keresztneve: {probaLista[0].Keresztnev}");

                // Kiírjuk az utolsó elem nevét
                Console.WriteLine("Utolsó ember keresztneve: " + probaLista[probaLista.Count - 1].Keresztnev);
```


---

# LAMBDA operátor FOREACH-ben

```ruby
namespace Dolgozok_Console_Winform
{
    class Program
    {
        static List<Dolgozo> dolgozok = new List<Dolgozo>();

            static void Main(string[] args)
        {
            beolvasas();
            feladat01(); //Hány fő dolgozó
            feladat02(); //Legmagasabb keresetű dolgozó neve
            feladat03(); //Egyes részlegeken hányan dolgoznak
            feladat04(); //Az asztalos műhelybe dolgozók neve

            //kiiras(dolgozok);
            Console.WriteLine("Program vége!");
            Console.ReadKey();
        }

        private static void feladat04()
        {
            Console.WriteLine("4. feladat:");
            foreach (var item in dolgozok.FindAll(x => x.reszleg == "asztalosműhely"))
            {
                Console.WriteLine($"\t{item.nev}");
            }
        }

        private static void feladat03()

        {

            Console.WriteLine("3. feladat:");

            foreach(var item in dolgozok.GroupBy(x => x.reszleg).Select(y => new {reszleg =y.Key , letszam = y.Count() } ))

            { 

                Console.WriteLine($"\t{item.reszleg}: {item.letszam}");

            }
        }
        private static void feladat02()

        {
            Console.WriteLine("2. feladat:");
            Dolgozo max = dolgozok.Find(x => x.ber == dolgozok.Max(y => y.ber)); //lambda operator
            Console.WriteLine($"\t A{max.nev} dolgozo fizetése:{max.ber} Ft");
        }
        private static void feladat01()
        {
            Console.WriteLine("1. feladat:");
            Console.WriteLine($"\t A dogozók száma {dolgozok.Count} fő.");
        }
        private static void kiiras(List<Dolgozo> dolgozok)
        {
            foreach (Dolgozo item in dolgozok)
            {
                Console.WriteLine(item.nev);
            }
        }

        private static void beolvasas()
        {
            string filename = "dolgozok.csv";
            using (StreamReader reader = new StreamReader(filename))
            {
                reader.ReadLine(); // fejléc átugrása
                while (!reader.EndOfStream)
                {

                    string[] line = reader.ReadLine().Replace('"',' ').Split(',');

                    Dolgozo dolgozo = new Dolgozo(line[0].Trim(), line[1].Trim(), line[2].Trim(), int.Parse(line[3].Trim()),int.Parse(line[4].Trim()));

                    dolgozok.Add(dolgozo);
                }
            }
        }
    }
}

```


---

---


# WinFORM - MySqlConnector & SQL adatok megjelenítése egy DATAGRID-ben

---

```ruby

using MySql.Data.MySqlClient;

public partial class Form1 : Form
{
    //deklarál egy MySqlConnection típusú változót, amely később az adatbáziskapcsolatot fogja képviselni
    MySqlConnection connection;

    public Form1()
    {
        InitializeComponent();


        //sql parancs meghatározása, amit le akarunk kérni:
        string sqlParancs = "SELECT rank, building_name, floors FROM buildings";

        //MySQL adatbázishoz való kapcsolat meghatározása:
        connection = new MySqlConnection("server=localhost;userid=root;password=;database=tallest_buildings");
        
        //kapcsolat nyitása:
        connection.Open();

        //MySqlDataAdapter a MySQL adatbázisokkal való munkavégzés során, adapterként szolgál,
        //lehetővé teszi az adatok lekérdezését és frissítését az adatbázis és a .NET alkalmazás között
        MySqlDataAdapter adapter = new MySqlDataAdapter(sqlParancs, connection);

        DataSet ds = new DataSet();
        adapter.Fill(ds);

        //datagridhez kell, hogy bekerüljön az adat:
        BindingSource bs = new BindingSource();
        bs.DataSource = ds.Tables[0];
        dataGridView1.DataSource = bs;

    }
}
```


---
---


# WinFORM - DATAGRID - TÖRLÉS adatbázisból és DataGridből is



```ruby

 private void buttonTorles_Click(object sender, EventArgs e)
 {
  
     if (dataGridView1.SelectedRows.Count > 0)
     {
         //az első oszlop tartalmazza az azonosítót (rank)
         int rank = Convert.ToInt32(dataGridView1.SelectedRows[0].Cells["rank"].Value);

         //SQL-ból TÖRLÉS parancsa:
         string sqlbolTorol = "DELETE FROM buildings WHERE rank = @rank";
         MySqlCommand command = new MySqlCommand(sqlbolTorol, connection);
         command.Parameters.AddWithValue("@rank", rank);

         // a törlés sql parancs végrehajtása
         int result = command.ExecuteNonQuery();

         if (result > 0)
         {
             //HA sikeres a törlés az adatbázisból,akkor távolítsuk el a sort a DataGrid-ből is!
             dataGridView1.Rows.RemoveAt(dataGridView1.SelectedRows[0].Index);
             MessageBox.Show("A kijelölt sor törölve az adatbázisból és a DataGridView-ból.");
         }
         else
         {
             MessageBox.Show("A sor törlése nem sikerült az adatbázisból.");
         }
     }
     else
     {
         MessageBox.Show("Kérlek, válassz ki egy EGÉSZ sort a törléshez.");
     }
```





# WinForm | osztályban alkalmazni | egy lista megjelenítésénél a nevét adja vissza:

```ruby
             public override string ToString()
             {
                 return megnevezes;
             }
```
