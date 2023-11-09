# Aufgabe B - Liveness, Readiness

## Links
- [Link zu den Ressourcen im GitLab](https://gitlab.com/ch-tbz-hf/Stud/v-cnt/-/tree/main/2_Unterrichtsressourcen/A)
- [Link zur Kubernetes-Oberfläche](https://10.5.38.10:8443/#/create?namespace=default)

## Readiness Befehl
Es kann schnell einmal passieren, dass eine Applikation, welche über längere Zeit lauft, zu einem beschädigten Zustanden wechselt und sich nicht mehr erholen kann, ohne neugestartet zu werden.
Mit Kubernetes können wir uns diese Fälle etwas vereinfachen. Kubernetes bietet uns die Möglichkeit, Lebenszeichen zu senden, damit wir von solchen Situationen schnell erfahren und reagieren können.

Mit dem folgenden Befehl können wir einen Pod erstellen, der einen Container ausführt:
