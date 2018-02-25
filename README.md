# Liederbuch Template

## Einleitung

Dieses Template ist im Rahmen der Jugendarbeit des Arbeitskreises Roverstufe des Diözesanverband Freiburg der Deutschen Pfadfinderschaft Sankt Georg zwischen 2017 und 2018 entstanden.
Viele Stunden sind in das zusammenfrickeln eines ansehbaren LateX-Templates geflossen. Es wäre schade, wenn nicht noch jemand anderes dieses nutzen könnte. Wenn dir auffällt, dass wir etwas hätten besser lösen können, freuen wir uns über deinen Input.

## Features

* **Inhaltsverzeichnis**
* **Kuraten Verzeichnis** - Das Kuratenverzeichnis ist ein zweites Inhaltsverzeichnis am Ende des Liederbuch. Hier können alle geistlichen Lieder aufgelistet werden, damit sie vor einer Morgenrunde/Gottesdienst/Impuls schneller gefunden werden.
* **Verweise** - Lieder können auf ihr vorkommen in anderen Liederbüchern verweisen. So kann auch mit einem gemischten Bestand an Liederbüchern gemütlich gesungen werden.
* **Auf der nächsten Seite geht es weiter Symbol** - Unerfahrenen Sängern kann es passieren, dass Sie nicht merken, das ein Lied eigentlich noch weitergeht. Einfach weil sich ein Zeilenumbruch eingeschlichen hat. EIn kleines Symbol am Ende einer Seite hilft hier weiter.
* **Jederzeit den Titel und Interpreten sehen** - Titel und Interpret findest du auf jeder Seite in der Kopfzeile. So findest du beim Durchblättern noch schneller das richtige Lied.

## Projektaufbau

### Liederbuch.tex

Die Hauptdatei. Hier wird das Layout festgelegt, benutzerdefinierte Befehle angelegt, die Struktur des Liederbuches definiert, Lieder eingebunden, ...

### bilder/...

Hier werden alle Bilder und grafischen Gestaltungselemente die in Liedern verwendet werden abgelegt.

### icons/...

Kleine Icons die im Layout verwendet werden, werden hier gespeichert.

### lieder/...

Alle Lieder die im Liederbuch verwendet werden, werden hier gespeichert. Einen Schwung Illustrationen haben wir hier schon abgespeichert. Bitte beachte die dort abgelegte LICENSE.md Datei wenn du sie verwenden möchtest.

## Lieder anlegen

Eine Lieddatei beginnt immer mit folgenden Header:

```tex
\def\Titel{Die Gedanken sind frei}
\def\Interpret{Deutsches Volkslied}
\def\Referenz{Möglicher Querverweis auf ein gebräuchliches Liederbuch deiner Wahl}

% hier entweder \LiedSetup() oder wenn es im Kuratenverzeichnis auftauchen soll \GeistlichSetup{}
\LiedSetup{}

\begin{guitarMagic}
```

* Der Parameter `\Titel` wird als Überschrift des Liedes verwendet, taucht in den Verzeichnissen auf und wird in der Kopfzeile auf der Blattaußenseite verwendet.
* Der Parameter `\Interpret` wird in der Kopfzeile auf der Falzseite verwendet.
* Der Parameter `\Referenz` wird in der Fußzeile auf der Falzseite verwendet und soll auf das Vorkommen dieses Liedes in anderen populären Liederbüchern verweisen.
* Der Befehl `\LiedSetup()` verwendet die vorherigen Parameter und stellt das richtige Layout sicher.
* Alternativ kann der Befehl `\GeistlichSetup()` verwendet werden. Zusätzlich zu `\LiedSetup()` wird ein damit eingeleitetes Lied noch im sekundären Inhaltsverzeichnis gelistet.
* Nach `\begin{guitarMagic}` kann das eigentliche Lied gesetzt werden.

```tex
    \begin{enumerate}

        \item Die Ge[A]danken sind frei, wer [E7]kann sie er[A]raten?\\
        Sie fliehen vorbei wie [E7]nächtliche [A]Schatten.\\
        Kein [E]Mensch kann sie [A]wissen, kein [E]Jäger er[A]schießen
        mit [D]Pulver und [A]Blei.\\
        Die Ge[E]danken sind [A]frei!

        \item Ich [A]denke, was ich will und [E]was mich be[A]glücket,\\
        doch alles in der Still’
        und [E]wie es sich [A]schicket.\\
        Mein [E]Wunsch und Be[A]gehren
        kann [E]niemand ver[A]wehren,
        es [D]bleibet da[A]bei:\\
        Die Ge[E]danken sind [A]frei!
        % So wird ein Seitenumbruch mit dem "auf der nächsten Seite gehts weiter" eingefügt
        \liedweiter{}


    \end{enumerate}
```

* Im Regelfall wird das Lied mit `\begin{enumerate}` begonnen. Jedes `\item` beginnt dann automatisch eine neue Strophe die der Reihe nach durchnummeriert werden.
* Eine Zeile wird mit einem `\\` beendet.
* Der Befehl `\liedweiter{}` sorgt dafür, dass ein "Lied geht auf der nächsten Seite weiter"-Zeichen eingefügt wird und eine neue Seite angefangen wird.
* Refrains werden wie folgt eingefügt.

```tex
Diese Strophe geht hier zu Ende.

\textbf{Refrain 1:}
Ich bin der Text des Refrains\\
```

* Sollte ein Lied mit einem Intro oder Refrain anstelle einer Strophe beginnen, muss dieser Teil des Stücks vor dem `\begin{enumerate}`, wie folgt stehen

```tex
\textbf{Intro:}
Introtext, geklimper und andere musikalischen Dinge

\begin{enumerate}
    \item Ich bin die erste Strophe nach dem Intro

```

* Gitarrenakkorde werden mit dem `Guitar`-Package gesetzt. Wie das geht darfst du selber nachlesen.

```tex
\end{guitarMagic}

% Bilder können nicht in der guitarmagic Umgebung eingefügt werden. Das muss davor oder danach geschehen
\begin{picture}(0,0)
    \put(-5,-150){\hbox{\includegraphics[scale=0.25, angle=0]{bilder/Flaschenpost.png}}}
\end{picture}
```

* Ein Lied endet mit dem `\end{guitarMagic}`-Befehl.
* Optional kann noch ein Bild eingebunden werden. Hierbei ist zu beachten, dass Bilder nicht in der `guitarMagic`-Umgebung verwendet werden können.