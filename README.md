# OpenBook E-Book Reader

Bine ați venit la proiectul OpenBook, un cititor de e-bookuri open-source, accesibil, conceput pentru a face lectura disponibilă tuturor. Acest repository conține fișierele de design hardware, fișierele de fabricație, modelele mecanice și documentația pentru dispozitivul OpenBook.

## Cuprins

- [Prezentare Proiect](#prezentare-proiect)
- [Diagramă Bloc](#diagrama-bloc)
- [Lista de Materiale (BOM)](#lista-de-materiale-bom)
- [Funcționalitate Hardware](#functionalitate-hardware)
- [Alocarea Pinilor ESP32-C6](#alocarea-pinilor-esp32-c6)
- [Note de Design](#note-de-design)
- [Licență](#licenta)

## Prezentare Proiect

OpenBook este un cititor de e-bookuri open-source bazat pe microcontrolerul ESP32-C6. Dispozitivul include un display e-paper, stocare pe card SD pentru e-bookuri, o interfață USB-C pentru alimentare și date, și un design compact care se potrivește într-o carcasă personalizată. Scopul este crearea unui e-reader ieftin, modificabil, care poate fi produs în masă, respectând principiile open-source.

Acest repository conține:

- **Hardware**: Fișiere pentru schemă electrică și PCB.
- **Manufacturing**: Fișiere Gerber, Lista de Materiale (BOM) și fișiere Pick and Place.
- **Mechanical**: Modele 3D ale dispozitivului complet (PCB, baterie, display și carcasă).
- **Images**: Randări ale PCB-ului și dispozitivului.

## Diagramă Bloc

Mai jos este o diagramă bloc care ilustrează componentele principale și conexiunile lor:

![Diagramă Bloc](Images/diagrama_bloc.png)

*(Notă: Creează o diagramă folosind Draw.io sau Lucidchart, export-o ca PNG și încarc-o în folderul `Images`. Actualizează link-ul de mai sus dacă numele fișierului este diferit.)*

## Lista de Materiale (BOM)

Tabelul următor listează componentele folosite în designul OpenBook, cu link-uri către furnizori și datasheet-uri.

| Componentă                | Număr Piesă                  | Cantitate | Link Furnizor                                                                 | Link Datasheet                                                                                                                                              | Note                              |
|---------------------------|------------------------------|-----------|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|
| Senzor mediu              | BME680                       | 1         | [SnapEDA](https://www.snapeda.com/parts/BME680/Bosch/view-part/?welcome=home)   | [Bosch](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf)                                                     | Senzor temperatură, umiditate     |
| Buton tactil              | EVQPUJ02K                    | 3         | [Panasonic](https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k) | [LCSC](https://www.lcsc.com/datasheet/lcsc_datasheet_2201121800_PANASONIC-EVQPUJ02K_C2936858.pdf)                              | Butoane navigare și pornire       |
| Condensator               | R0402 100K                   | [TBD]     | [ComponentSearch](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO) | [Resistor](https://www.resistor.com/assets/pdf/0402tstd.pdf)                                                                 | Condensator decuplare, SMD 0402   |
| Rezistor                  | R0402 100K                   | [TBD]     | [ComponentSearch](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO) | [Resistor](https://www.resistor.com/assets/pdf/0402tstd.pdf)                                                                 | Rezistor, SMD 0402                |
| Baterie                   | CPH3225A                     | 1         | [SnapEDA](https://www.snapeda.com/parts/CPH3225A/Seiko+Instruments/view-part/?ref=eda) | [Octopart](https://octopart.com/datasheet/cph3225a-seiko-25340571)                                                                  | Baterie Li-Po, ~500mAh            |
| LED                       | KP-1608SURCK                 | 1         | [SnapEDA](https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/view-part/?ref=search&t=LED%200603) | [ELV](https://media.elv.com/file/107153_led_surck1608_data.pdf)                                                                     | LED 0603, indicator               |
| Protecție ESD             | USBLC6-2SC6Y                 | 1         | [SnapEDA](https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=eda) | [DigiKey](https://www.digikey.com/en/htmldatasheets/production/1375342/0/0/1/usblc6-2sc6y)                                          | Protecție USB                     |
| Diodă Schottky            | SD0805S020S1R0               | 1         | [Mouser](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D) | [AllDataSheet](https://www.alldatasheet.com/view.jsp?Searchword=SD0805S&sField=2)                                                    | Diodă pentru alimentare           |
| Supresor ESD              | PGB1010603MR                | 1         | [SnapEDA](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda) | [AllDataSheet](https://www.alldatasheet.com/view.jsp?Searchword=Pgb1010603mr)                                                        | Protecție ESD                     |
| Detector tensiune         | BD5229G-TR                   | 1         | [ComponentSearch](https://componentsearchengine.com/part-view/BD5229G-TR/ROHM%20Semiconductor) | [LCSC](https://www.lcsc.com/datasheet/lcsc_datasheet_2201131330_ROHM-Semicon-BD5229G-TR_C962636.pdf)                         | Monitorizare tensiune             |
| Regulator tensiune        | XC6220A331MR-G               | 1         | [ComponentSearch](https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex) | [AllDataSheet](https://www.alldatasheet.com/view.jsp?Searchword=Xc6220)                                                              | Regulator 3.3V                    |
| Conector USB-C            | USB4110-GF-A                 | 1         | [ComponentSearch](https://componentsearchengine.com/part-view/USB4110-GF-A/GCT%20(GLOBAL%20CONNECTOR%20TECHNOLOGY)) | [GCT](https://gct.co/files/drawings/usb4110.pdf)                                                                            | Interfață USB-C                   |
| LED                       | LEDCHIP-LED0603              | 1         | [Mouser](https://eu.mouser.com/ProductDetail/Adafruit/4208?qs=PzGy0jfpSMtbScLbr0L5dw%3D%3D) | [Arrow](https://www.arrow.com/en/manufacturers/adafruit-industries/datasheets)                                              | LED 0603, Adafruit                |
| Bobină                    | [TBD]                        | 1         | [Comet](https://store.comet.srl.ro/Catalogue/Product/43497/)                           | [Scribd](https://www.scribd.com/document/814581278/Datasheet-Bobina)                                                                | Inductor pentru alimentare        |
| Siguranță resetabilă      | PFMF                          | 1         | [Mouser](https://www.mouser.co.uk/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D) | [Mouser](https://ro.mouser.com/c/ds/circuit-protection/thermistors/resettable-fuses-pptc/?m=Schurter&series=PFMF)             | Protecție circuit                 |
| MOSFET                    | DMG2305UX-7                  | 1         | [ComponentSearch](https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated) | [Mouser](https://www.mouser.com/datasheet/2/115/DMG2305UX-266242.pdf)                                                       | Comutare putere                   |
| MOSFET                    | Si1308EDL-T1-GE3             | 1         | [ComponentSearch](https://componentsearchengine.com/part-view/SI1308EDL-T1-GE3/Vishay) | [AllDataSheet](https://www.alldatasheet.com/view.jsp?Searchword=Si1308edl)                                                   | Comutare putere                   |
| IC management baterie     | MCP73831T-5ACI/OT            | 1         | [Mouser](https://www.mouser.co.uk/ProductDetail/Microchip-Technology/MCP73831T-5ACI-OT?qs=hH%252BOa0VZEiAcgAcEkuamXg%3D%3D) | [Microchip](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP73831-Family-Data-Sheet-DS20001984H.pdf)                     | Încărcare baterie                 |
| Lipire SMD                | SMD Solder                   | [TBD]     | [GrabCAD](https://grabcad.com/library/solder-jumpers-1)                                | -                                                                                                                                                           | Pentru asamblare SMD              |
| Memorie flash             | W25Q512JVEIQ                 | 1         | [SnapEDA](https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/) | [Mouser](https://www.mouser.com/datasheet/2/949/W25Q512JV_SPI_RevB_06252019_KMS-2487502.pdf)                                | Memorie SPI                       |
| Modul microcontroler      | ESP32-C6-WROOM-1-N8          | 1         | [SnapEDA](https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif+Systems/view-part/?ref=eda) | [Mouser](https://www.mouser.com/catalog/specsheets/Espressif_ESP32_C6_WROOM_1%20_Datasheet_V0.1_PRELIMINARY_en.pdf)         | Modul Wi-Fi/Bluetooth             |
| Ceas timp real            | DS3231SN#                    | 1         | [SnapEDA](https://www.snapeda.com/parts/DS3231SN%23/Analog+Devices/view-part/?ref=eda) | [AllDataSheet](https://www.alldatasheet.com/view.jsp?Searchword=Ds3231sn%20datasheet)                                        | RTC pentru timp                   |
| Monitor baterie           | MAX17048G+T10                | 1         | [SnapEDA](https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=eda) | [AllDataSheet](https://www.alldatasheet.com/view.jsp?Searchword=Max17048)                                                    | Monitorizare nivel baterie        |



## Funcționalitate Hardware

Hardware-ul OpenBook este proiectat pentru a echilibra costul, eficiența energetică și funcționalitatea. Caracteristicile principale includ:

- **Microcontroler ESP32-C6**:
  - **Nucleu**: Procesor RISC-V single-core.
  - **Conectivitate**: Wi-Fi 6 și Bluetooth 5 pentru actualizări de firmware sau integrare cloud.
  - **Interfețe**: SPI pentru display și card SD, GPIO pentru butoane, USB pentru alimentare și depanare.
  - **Consum de energie**: Optimizat pentru funcționare cu consum redus, cu moduri de sleep pentru a prelungi durata bateriei.

- **Display E-Paper**:
  - Display e-paper de 2.13" (rezoluție [TBD, ex. 250x122 pixeli]).
  - Conectat prin SPI pentru actualizare rapidă și consum redus.
  - Ideal pentru citit în diverse condiții de iluminare, cu consum minim.

- **Modul Card SD**:
  - Stochează e-bookuri și alte fișiere media.
  - Conectat prin SPI pentru transfer de date fiabil.
  - Suportă carduri microSD standard.

- **Interfață USB-C**:
  - Furnizează alimentare (intrare 5V) și încarcă bateria prin IC-ul de management al puterii.
  - Suportă transfer de date pentru depanare sau actualizări de firmware.

- **Baterie și Management Putere**:
  - Baterie Li-Po de 3.7V (~500mAh, capacitate exactă [TBD]).
  - IC de management al puterii (ex. TP4056) gestionează încărcarea și reglarea tensiunii (3.3V pentru ESP32 și alte componente).
  - Durata estimată a bateriei: [TBD, ex. 20 ore de citire activă], bazată pe calcule pentru actualizarea display-ului, modurile sleep ale ESP32 și accesul la cardul SD.

- **Butoane**:
  - Trei butoane tactile pentru navigare (următoarea/pagina anterioară) și pornire/meniu.
  - Conectate la pinii GPIO ai ESP32 cu rezistoare pull-up.

- **Calcule Consum Energie**:
  - ESP32-C6 (activ): ~100mA la 3.3V.
  - Display E-Paper (actualizare): ~10mA pentru 1s per pagină.
  - Card SD (citire): ~50mA în timpul accesului.
  - Consum total activ: [TBD, ex. ~150mA mediu].
  - Mod sleep: [TBD, ex. <1mA].

*(Notă: Actualizează consumul de energie și alte specificații pe baza alegerilor tale de design și a datasheet-urilor.)*

## Alocarea Pinilor ESP32-C6

Pinii ESP32-C6 sunt alocați astfel:

| Pin       | Funcție                 | Componentă/Modul        | Note                              |
|-----------|-------------------------|-------------------------|-----------------------------------|
| GPIO0     | SPI MOSI                | Display E-Paper, Card SD| Bus SPI comun                     |
| GPIO1     | SPI MISO                | Display E-Paper, Card SD| Bus SPI comun                     |
| GPIO2     | SPI SCK                 | Display E-Paper, Card SD| Bus SPI comun                     |
| GPIO3     | SPI CS (Display)        | Display E-Paper         | Selectare cip pentru display      |
| GPIO4     | SPI CS (Card SD)        | Modul Card SD           | Selectare cip pentru card SD      |
| GPIO5     | Buton 1 (Pagina Urm.)   | Buton Tactil            | Pull-up, activ low                |
| GPIO6     | Buton 2 (Pagina Ant.)   | Buton Tactil            | Pull-up, activ low                |
| GPIO7     | Buton 3 (Pornire/Meniu) | Buton Tactil            | Pull-up, activ low                |
| GPIO8     | Reset Display           | Display E-Paper         | Activ low                         |
| GPIO9     | Busy Display            | Display E-Paper         | Intrare de la display             |
| VBUS      | Alimentare USB          | Conector USB-C          | Intrare 5V                        |
| 3V3       | Linie Alimentare        | Toate componentele      | Reglat din baterie/USB            |

*(Notă: Verifică alocarea pinilor față de schemă. Actualizează tabelul cu numerele exacte ale pinilor și funcțiile pe baza designului tău.)*

### De ce acești pini?

- **Pini SPI (GPIO0-4)**: Aleși pentru suportul hardware dedicat SPI, asigurând comunicație rapidă și fiabilă cu display-ul și cardul SD. Un bus SPI comun minimizează utilizarea pinilor.
- **Pini Butoane (GPIO5-7)**: Selectați pentru capabilitățile de intrare generală și suport pentru întreruperi, permițând interacțiune rapidă cu utilizatorul.
- **Pini Control Display (GPIO8-9)**: Folosiți pentru semnalele de reset și busy, conform cerințelor datasheet-ului display-ului e-paper.
- **Pini Alimentare (VBUS, 3V3)**: Standard pentru livrarea și reglarea energiei.

## Note de Design

- **Schemă și Design PCB**:
  - Schema (`Hardware/openbook.sch`) respectă referința furnizată.
  - Layout-ul PCB (`Hardware/openbook.brd`) respectă constrângerile mecanice, cu toate componentele pe stratul TOP și rutarea pe ambele straturi TOP și BOTTOM.
  - Traseele de alimentare folosesc lățimea de 0.3mm, iar traseele de semnal au lățimea minimă de 0.15mm, conform ghidului.
  - Antena ESP32-C6 este poziționată la marginea PCB-ului, cu o decupare dedesubt pentru a minimiza interferențele.

- **Design Mecanic**:
  - Modelul 3D (`Mechanical/openbook.step`) include PCB-ul, bateria, display-ul e-paper și carcasa modificată.
  - Bateria se conectează direct la pad-uri de test (fără conector JST) pentru a economisi spațiu.
  - Carcasa a fost modificată pentru a alinia portul USB-C și slotul pentru card SD (detalii în folderul `Mechanical`).

- **Provocări și Decizii**:
  - **erori DRC**: Ignorate erorile „Only INPUT pins on NET ID” și erorile de dimensiune pentru butoane/USB, conform ghidului, deoarece nu afectează funcționalitatea.
  - **Amplasare componente**: Componentele au fost grupate în jurul ESP32 și al driverului display-ului pentru a minimiza lungimea traseelor și a îmbunătăți integritatea semnalului.
  - **Via Stitching**: Aplicat între planurile de masă TOP și BOTTOM lângă ESP32 pentru a îmbunătăți performanța EMI.
  - **Silkscreen**: Include doar numele componentelor (nu și valorile) pentru claritate, respectând bunele practici.


## Licență

Acest proiect este licențiat sub [GNU General Public License v3.0](LICENSE). Puteți utiliza, modifica și distribui designul, cu condiția respectării termenilor licenței.
