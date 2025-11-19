# codesys-portfolio

🚦 TrafficLight – Közlekedési lámpa vezérlő (CODESYS)

A TrafficLight egy CODESYS-alapú PLC-projekt, amely két klasszikus közlekedési lámpa teljes vezérlését valósítja meg. A projekt demonstrálja a Structured Text állapotgépet, az időzítők használatát, a vizualizáció (HMI) lehetőségeit és a Modbus TCP integrációt.

Funkciók:
  1.) Komplett lámpaszekvencia:
    - Piros → Piros–sárga → Zöld → Sárga ciklusok
    - Fault / hibakezelés
    - Semleges állapot
    
  2.) Moduláris programfelépítés:
    - TrafficLight_FB: a lámpa állapotgépének logikája
    - GVL_TL: globális változók
    - PLC_PRG: a projekt fő rutinja (FB hívás, vizualizáció támogatás)

  3.) HMI / Visualisation:
    - Start / Stop / Fault gombok
    - Lámpák vizualizációja
    - Állapotkijelzés, timer értékek

  4.) Modbus TCP integráció:
    - Idők (Red / Yellow / Green) beolvashatók Holding Registerekből
    - PLC változók Modbus-regiszterekhez rendelve

Felépítés:
  PLC-CODESYS/
    └── TrafficLight/
        ├── PLC_PRG          – fő program
        ├── TrafficLight_FB  – funkcióblokk (állapotgép)
        ├── GVL_TL           – globális változók
        ├── Visualization    – HMI felület
        └── ModbusTCP        – opcionális kommunikációs interfész

Technikai részletek:
  - Programnyelv: Structured Text (ST)
  - Időzítők: TON
  - Állapotgép: CASE szerkezet
  - Vizualizáció: dinamikus színváltás (BOOL → fill color)
  - Kommunikáció: HMI és Modbus TCP (opcionális)
