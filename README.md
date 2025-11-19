# codesys-portfolio

🚦 TrafficLight – Közlekedési lámpa vezérlő (CODESYS)

A TrafficLight egy CODESYS-alapú PLC-projekt, amely két klasszikus közlekedési lámpa teljes vezérlését valósítja meg. A projekt demonstrálja a Structured Text állapotgépet, az időzítők használatát, a vizualizáció (HMI) lehetőségeit és a Modbus TCP integrációt.

~ Funkciók

Komplett lámpaszekvencia:
  - Piros → Piros–sárga → Zöld → Sárga ciklusok
  - Fault / hibakezelés
  - Semleges állapot

Moduláris programfelépítés:
  - TrafficLight_FB: a lámpa állapotgépének logikája
  - GVL_TL: globális változók
  - PLC_PRG: a projekt fő rutinja (FB hívás, vizualizáció támogatás)

HMI / Visualisation:
  - Start / Stop / Fault gombok
  - Lámpák vizualizációja
  - Állapotkijelzés, timer értékek

Modbus TCP integráció:
  - Idők (Red / Yellow / Green) beolvashatók Holding Registerekből
  - PLC változók Modbus-regiszterekhez rendelve

~ Felépítés:
    PLC-CODESYS/
      └── TrafficLight/
              ├── PLC_PRG          – fő program
              ├── TrafficLight_FB  – funkcióblokk (állapotgép)
              ├── GVL_TL           – globális változók
              ├── Visualization    – HMI felület
              └── ModbusTCP        – opcionális kommunikációs interfész

~ Technikai részletek:
  - Programnyelv: Structured Text (ST)
  - Időzítők: TON
  - Állapotgép: CASE szerkezet
  - Vizualizáció: dinamikus színváltás (BOOL → fill color)
  - Kommunikáció: HMI és Modbus TCP (opcionális)

~ Leírás:
  - A "START" gomb megnyomásáig a lámpák semleges állapotban maradnak, azaz sárgán villognak.
  - A "START" gomb megnyomása indítja a normál üzemet, a lámpák ciklikus működését. Mielőtt a lámpák belépnének ezen ismétlődő ciklusaikba, egyszer végigmennek az indítás utáni procedúrán: sárga villogás, majd mindkét lámpa piros a beállított időtartamokra.
  - A "FAULT" gomb megnyomása üzemzavar állapotba teszi a lámpákat: sárga villogás.
  - A "MODE SELECT" felkapcsolásával (TRUE) a kommunikáció Modbus TCP szerveren keresztül megy végbe, alapesetben (FALSE) HMI-n keresztül. Modbus módban tehát a kívülről (pl. Modbus Poll által) megadott értékekkel futnak a program időzítői, HMI módban pedig az írható táblázatban lehet megadni az időzítők értékeit. Maximum érték: 65535, mértékegység: ms.
