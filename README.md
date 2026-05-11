# DUMMY / RaspTank Voice Robot

- **Cel projektu:** autonomiczno-zdalnie sterowany robot gąsienicowy z kamerą, chwytakiem i sterowaniem głosowym. Komendy głosowe są zamieniane na intencje, a następnie na konkretne akcje robota, np. jazdę, skręt, ruch kamery lub chwytaka.

- **Baza sprzętowa:** robot jest zbudowany na elektrycznych komponentach zestawu **Adeept RaspTank2**. Części plastikowe są w ok. **98% zaprojektowane przeze mnie** i wykonane na drukarce 3D.

- **NLU (Natural Language Understanding):** warstwa rozumienia języka naturalnego interpretuje tekst z komendy głosowej i rozpoznaje intencję użytkownika, np. `motion.forward`, `camera.left`, `gripper.grab` albo `system.stop`.

- **SetFit (Machine Learning):** lokalny model AI używany do klasyfikacji intencji komend głosowych. Model znajduje się w katalogu `robot_nlu_model/` i pozwala sterować robotem za pomocą **dowolnej, nie przewidzianej wcześniej komendy**.

- **ITF (Intent-to-Function):** logika mapowania intencji na funkcje robota. Dzięki temu wynik NLU jest zamieniany na realne akcje: ruch silników, sterowanie kamerą, obsługę chwytaka, pozycję domową lub zatrzymanie awaryjne.

- **Python + Flask:** backend robota, endpoint `POST /parse`, serwer strony `/voice`, obsługa kamery, ruchu, serw, czujnika ultradźwiękowego i komunikacji z interfejsem webowym.

- **Web UI / sterowanie głosowe:** strona `web/voice_ui/voice.html` korzysta z mikrofonu w przeglądarce, wysyła rozpoznany tekst do Raspberry Pi i pokazuje wynik interpretacji komendy.

- **Czujnik ultradźwiękowy:** podczas jazdy do przodu robot sprawdza przeszkody i może wykonać procedurę omijania zamiast jechać bezpośrednio w obiekt.

- **Autorstwo i zakres zmian:** kod jest wzorowany na projekcie Adeept RaspTank2, ale zdecydowana większość implementacji została napisana przeze mnie. W szczególności **wszystkie pliki Python w tej wersji są moją implementacją lub gruntowną przebudową**, a oryginalny projekt Adeept nie posiadał sterowania głosowego ani warstwy AI/NLU.

- **Główne pliki projektu:**
  - `run_tank_voice.sh` — uruchomienie robota i strony sterowania głosowego,
  - `web/webServer.py` — główna logika sterowania, NLU, ITF i endpoint `/parse`,
  - `web/voice_ui/voice.html` — interfejs sterowania głosowego,
  - `robot_nlu_model/` — lokalny model SetFit,
  - `VOICE_CONTROL_PL.md` / `VOICE_CONTROL_EN.md` — instrukcja uruchomienia i przykładowe komendy.

- **Uruchomienie:**
  ```bash
  cd ~/DUMMY
  chmod +x run_tank_voice.sh
  ./run_tank_voice.sh
  ```
  Następnie w przeglądarce: `http://IP_RASPBERRY:5000/voice`.
