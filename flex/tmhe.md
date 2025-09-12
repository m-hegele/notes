# ChargeHere x TMHE
- TMHE
    - Eigene DC Wallbox
    - V2G mit Mercedes

- Schnittstelle zwischen THMe-Aggregarionsplattform und unserem System (hier würde uns auch eine Schnittstellenspezifikation als OpenAPI-Dokument o.ä. genügen)
    - Spec folgt
    - Charging efficiency
- Welche Prognosegenauigkeit wird verlangt / empfohlen?
    - 36h Voraus
    - Korrektur bis 5 Minuten vor Erfüllung möglich
    - Muss festgelegt werden
    - Value-Share & Risk-Share

- Wie wird mit Prognoseabweichungen verfahren?
    - Risk Sharing
    - Risikopuffer für MVP
    - Einigung von Prognosegenauigkeit & Abweichung = Malus

- Wie werden Assents optimiert? Day-Ahead, Intraday, FCR, FRR, Redispatch
    - höchster Mehrwert im Wholesale-Trading (DA, IA, IC)
    - 7-10 x Trading pro Position (tatsächliches Laden)
    - möglich: variable Netzentgelte (Local-flex), aber kann auch von uns übernommen werden (Behind-the-Meter Optimierungen)
    - FCR, FRR, Redispatch: nur Batteriespeicher aktuell
- Welche Mehrwerte können beispielhaft in Mehrfamilienhäusern und an Unternehmensstandorten (Flotten und Mitarbeiterladen) erreicht werden?
    - Personas & Bänder
    - Shared Revenue Modell
    - Tolling offer, e.g. 3 ct pro smart charged kWh
- Wie sieht das pricing aus?
- Kann über Standorte hinweg voraggregiert werden? Z.B. alle internen EnBW-Ladepunkte
    - Bilanzkreis entscheidend


- Konstellation: TMHE x EnBW x ChargeHere
    - EnBW = Energieversorger (physisch)
    - Beschaffung durch TMHE
    - Fahrplanausgleich mit EnBW (auf kurzfristigen Märkten)
    - TMHE hat gekauft aber nicht geliefert, EnBW hat geliefert aber nicht gekauft