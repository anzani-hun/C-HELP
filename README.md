---

# CSV fájlban, ha van fejléc akkor:

`sr.ReadLine();`

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
