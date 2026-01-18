# Labeling Policy

Dieses Dokument beschreibt die verbindlichen Regeln und Best Practices für das Labeling von LiDAR- und Kameradaten. Ziel ist eine konsistente, qualitativ hochwertige Annotation über alle Szenen hinweg.

---

## Allgemeine Labeling-Regeln

- **Keine Bodenpunkte im Objekt**  
  Objekte dürfen keine Bodenpunkte enthalten. Der Boden soll unter Objekten (z.B. Straße unter Fahrzeugen) konsistent durchlaufen.

- **Tight Bounding Boxes**  
  Boxen sollten so eng wie möglich um die Punktwolke gezogen werden, ohne relevante Objektpunkte auszuschließen.

- **Nur reale Punkte einschließen**  
  Objekte dürfen ausschließlich tatsächlich vorhandene LiDAR-Punkte einschließen.  
  *Ausnahme:* Statische Objekte (z.B. Gebäude, Masten), bei denen eine leichte Generalisierung zulässig ist.

- **LiDAR vor Kamera**  
  Entscheidungen werden primär auf Basis der LiDAR-Daten getroffen, nicht anhand der Kamerabilder.

- **Keine Pseudo-Boxen**  
  Bounding Boxes dürfen nur auf der Punktwolke basieren. Keine Ergänzungen oder Größenabschätzungen aus dem Kamerabild.

- **Verschattung**  
  Verschattungen oder Teilverdeckungen erzeugen **keine** zusätzlichen Objekte. Es bleibt eine Instanz.

- **Klassenschema**  
  Klassen werden strikt nach dem **[8+1-Klassenschema](media/Bast_8plus1.pdf)** vergeben.

- **Minimale Punktanzahl**  
  Ein Objekt muss mindestens aus **einem** LiDAR-Punkt bestehen, um gelabelt zu werden.

---

## Frame Selection

- **Keine leeren Szenen**  
  Es werden nur Frames mit **dynamischen Objekten** gelabelt.

- **Kamera optimal nutzen**  
  Wenn möglich, Frames auswählen, in denen Fahrzeuge und Infrastruktur nah beieinander liegen, um Kamerainformationen sinnvoll zu unterstützen.

---

## Workflow

### 1. Tower priorisieren

- Zuerst **statische Objekte** identifizieren (z. B. parkende Autos).
- Frames auswählen, in denen sich das Ego-Fahrzeug nahe an diesen statischen Objekten befindet, um eine präzise Annotation zu ermöglichen.
- Anschließend die **Kopierfunktion** nutzen, um die Annotationen über die komplette Szene zu übertragen (`Alt + ← / →`).
- Danach verbleiben hauptsächlich **dynamische Objekte**.

### 2. Dynamische Objekte labeln

- Dynamische Objekte mit der **Tracking-Funktion** annotieren.
- In einem klaren Manöver beginnen und das Objekt logisch in den folgenden Frames wiederfinden.
- Alle dynamischen Objekte **strukturiert und vollständig** durch die Szene tracken.

### 3. Vehicle Handling

- Instanzen, die ausschließlich am Ego-Fahrzeug sichtbar sind (LiDAR-Punkte sind ausschlaggebend), werden entfernt.
- Das Ego-Fahrzeug kann anschließend als **separate Instanz** bearbeitet werden.

---

## Best Practices

- **Color Encoding** nutzen, um Bodenpunkte leichter zu identifizieren und zu separieren.
- Nach der Frame-Annotation alle Bilder prüfen, um sicherzustellen, dass keine Instanzen fehlen.
- Nach Kamera-Checks Straßen und Gehwege kontrollieren:
  - Objekte aus vergangenen oder folgenden Frames sinnvoll tracken.
- **Shortcuts** konsequent nutzen, um effizient zu arbeiten.
- **Regelmäßig speichern**, um Datenverlust zu vermeiden.

---

## Ziel

Konsistente, reproduzierbare und qualitativ hochwertige Labels über alle Szenen hinweg, mit Fokus auf LiDAR-basierter Genauigkeit und sauberem Tracking.


