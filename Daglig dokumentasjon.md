# 📘 Daglig dokumentasjon for prøve fagprøve

---

## 📅 2/5-2026

Skrev ferdig planleggings biten for prøve fagprøven, lagde datamodell for korleis eg vil ha databasen satt opp.
Lagde ein grov skisse for korleis eg vil at appen skal se ut.

---

## 📅 2/6-2026

Lagde tabeller, fikset security checks i triggers og atbv-er.

Hadde ikkje tilgang til å legge til tabeller i ein modul så eg måtte lage ein egen rolle som heter
`quiz developer` som har capibiltien **“Can administrate system modules”**,

også la eg rollen eg nettopp lagde i **“can grant”** inne i system administrator.,
også gidde eg meg sjølv quiz developer rollen.

Har begynnt på både dashbord siden og quiz siden til quiz appen.

---

## 📅 2/7-2026

...

---

## 📅 2/8-2026

Fikset next knappen, nå kan du bla til de neste spørsmålene i quizzen

---

## 📅 2/9-2026

Lagde ein retry knapp som vises når du er på siste spørsmål, også fikset eg UI på quizpage siden.

Lagde ein scoreboard tab, der ein proc skytes av når man er på siste spørsmål og lagres i ein tabell.

Også lagde eg ein "developer" tab for quizzene der alle som har quiz developer rolla kan gå inn og redigere quizenne, spørsmål, og svar.

Denne tabben skjules for folk uten denne rollen.
<img width="751" height="1148" alt="image" src="https://github.com/user-attachments/assets/c57aad6d-fe9c-4237-b401-2091f4ba104c" />


---

## 📅 2/10-2026

  Fekk ein endring idag, skal legge til kategorier per quiz, også skal man greie å filtrere på kvar kategori.
  Lagde ein ny tabell som heter atbl_HaakonStokkenes_QuizCategories der atbl_HaakonStokkenes_Quizes har ein foreign key mot categories tabellen.
  Gjorde ferdig quizpage siden, tok vekk at eg har 2 knapper og heller når man klikker på submit så får du svar, også skifter knappen navn til next.
  Begynnte på result skjermen.

---

## 📅 2/11-2026

  Istedenfor å ha ein satt verdi på poeng så la eg til ScoreIncrease og ScoreDecrease i questions tabellen, også bruker eg heller dei verdiene i kalkulasjonen
  Gjorde endringer på result skjermen, fikset UI, og la til mulighet for å åpne ein rapport som er et "quiz diploma"

---

## 📅 2/12-2026
Skrevet system dokumentasjon, bruker veiledning, og testrapport/fikset små feil i appen
