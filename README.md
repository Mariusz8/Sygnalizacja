# 🚦 Sygnalizacja świetlna Arduino UNO

 Projekt przedstawia prostą **sygnalizację świetlną dla 4 kierunków**, zrealizowaną na płytce **Arduino UNO**. Każdy kierunek posiada dwie diody LED: **czerwoną** i **zieloną**.

 Układ został zaprogramowany tak, aby kolejne kierunki otrzymywały światło zielone, podczas gdy pozostałe pozostają na czerwonym.

 ## 🧰 Wykorzystane elementy

 - Arduino UNO
- 4 × czerwona dioda LED
- 4 × zielona dioda LED
- 8 × rezystor ograniczający prąd
- przewody połączeniowe
- płytka stykowa / układ połączeń

 ## 🔌 Podłączenie

 Diody zostały podłączone do następujących pinów Arduino:

 | Kierunek | Czerwona LED | Zielona LED |
| --- | --- | --- |
| 1 | D2 | D3 |
| 2 | D4 | D5 |
| 3 | D6 | D7 |
| 4 | D8 | D9 |

Każda dioda LED powinna posiadać **rezystor ograniczający prąd**.

 ## ⚙️ Zasada działania

 Program działa w sposób cykliczny:

 1. Wszystkie cztery kierunki otrzymują światło **czerwone przez 2 sekundy**.
2. Kierunek 1 otrzymuje światło **zielone przez 5 sekund**.
3. Ponownie wszystkie kierunki są czerwone przez 2 sekundy.
4. Kierunek 2 otrzymuje światło zielone przez 5 sekund.
5. Następnie analogicznie kierunek 3.
6. Na końcu kierunek 4.
7. Po zakończeniu cyklu program wraca do początku.

 Dzięki funkcji `wszystkieCzerwone()` przed każdym przełączeniem zapewniony jest moment, w którym wszystkie kierunki mają czerwone światło.

 ## 💻 Kod programu

```
int czerwone1 = 2;
int zielone1 = 3;

int czerwone2 = 4;
int zielone2 = 5;

int czerwone3 = 6;
int zielone3 = 7;

int czerwone4 = 8;
int zielone4 = 9;

void setup() {
  pinMode(czerwone1, OUTPUT);
  pinMode(zielone1, OUTPUT);

  pinMode(czerwone2, OUTPUT);
  pinMode(zielone2, OUTPUT);

  pinMode(czerwone3, OUTPUT);
  pinMode(zielone3, OUTPUT);

  pinMode(czerwone4, OUTPUT);
  pinMode(zielone4, OUTPUT);
}

// Wszystkie światła czerwone przez 2 sekundy
void wszystkieCzerwone() {
  digitalWrite(czerwone1, HIGH);
  digitalWrite(czerwone2, HIGH);
  digitalWrite(czerwone3, HIGH);
  digitalWrite(czerwone4, HIGH);

  digitalWrite(zielone1, LOW);
  digitalWrite(zielone2, LOW);
  digitalWrite(zielone3, LOW);
  digitalWrite(zielone4, LOW);

  delay(2000);
}

void loop() {

  // 1
  wszystkieCzerwone();

  digitalWrite(czerwone1, LOW);
  digitalWrite(zielone1, HIGH);

  delay(5000);

  digitalWrite(zielone1, LOW);
  digitalWrite(czerwone1, HIGH);

  // 2
  wszystkieCzerwone();

  digitalWrite(czerwone2, LOW);
  digitalWrite(zielone2, HIGH);

  delay(5000);

  digitalWrite(zielone2, LOW);
  digitalWrite(czerwone2, HIGH);

  // 3
  wszystkieCzerwone();

  digitalWrite(czerwone3, LOW);
  digitalWrite(zielone3, HIGH);

  delay(5000);

  digitalWrite(zielone3, LOW);
  digitalWrite(czerwone3, HIGH);

  // 4
  wszystkieCzerwone();

  digitalWrite(czerwone4, LOW);
  digitalWrite(zielone4, HIGH);

  delay(5000);

  digitalWrite(zielone4, LOW);
  digitalWrite(czerwone4, HIGH);
}
```

 ## ⏱️ Harmonogram działania

 | Etap | Kierunek 1 | Kierunek 2 | Kierunek 3 | Kierunek 4 | Czas |
| --- | --- | --- | --- | --- | --- |
| 1 | 🔴 | 🔴 | 🔴 | 🔴 | 2 s |
| 2 | 🟢 | 🔴 | 🔴 | 🔴 | 5 s |
| 3 | 🔴 | 🔴 | 🔴 | 🔴 | 2 s |
| 4 | 🔴 | 🟢 | 🔴 | 🔴 | 5 s |
| 5 | 🔴 | 🔴 | 🔴 | 🔴 | 2 s |
| 6 | 🔴 | 🔴 | 🟢 | 🔴 | 5 s |
| 7 | 🔴 | 🔴 | 🔴 | 🔴 | 2 s |
| 8 | 🔴 | 🔴 | 🔴 | 🟢 | 5 s |

Po ostatnim etapie program rozpoczyna cały cykl od początku.

 ## 📌 Podsumowanie

 Projekt pokazuje podstawowe sterowanie diodami LED za pomocą Arduino UNO. Wykorzystano:

 - `pinMode()` – do ustawienia pinów jako wyjścia,
- `digitalWrite()` – do włączania i wyłączania diod,
- `delay()` – do ustalania czasu świecenia,
- własną funkcję `wszystkieCzerwone()` – do uproszczenia programu i zapewnienia 2-sekundowej fazy, w której wszystkie światła są czerwone.
