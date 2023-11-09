# Aufgabe B - Liveness, Readiness

## Links
- [Link zu den Ressourcen im GitLab](https://gitlab.com/ch-tbz-hf/Stud/v-cnt/-/tree/main/2_Unterrichtsressourcen/A)
- [Link zur Kubernetes-Oberfläche](https://10.5.38.10:8443/#/create?namespace=default)

## Readiness Befehl
Anders als beim Liveness, geht es nicht darum, dass eine Applikation in den beschädigten Zustand gerät, sondern darum, dass es vorübergehend nicht in der Lage ist, auf den Datenverkehr zu antworten oder diesen zu bedienen.
Wir kennen dies auch beim Aufstarten vom Computer, wenn einige Applikationen grosse Daten laden müssen oder von anderen Applikationen abhängig sind. In solchen Fällen, will man ja diese Applikation, welche vorübergehend verhindert ist, 
weder beenden, noch weitere Anfragen senden. Genau hierführ können wir die Readiness Probe von Kubernetes verwenden. Wir können ein Pod mit Containern erstellen, die Meldung von sich geben, dass sie nicht bereit sind.
Somit empfängt es dann auch keinen Datenverkehr über Kubernetes Dienste.

Die Readiness Probe ist ziemlich ähnlich wie die Liveness Probe, daher ist es auch von Vorteil, die beiden in einer Aufgabe zu behandeln. Wie wir im Liveness Befehl gesehen haben, machten wir vom Feld ```yaml livenessProbe``` gebraucht.
Im Readiness Befehl brauchen wir jedoch das Feld ```yaml readinessProbe```. 

```yaml
readinessProbe:
  exec:
    command:
    - cat
    - /tmp/healthy
  initialDelaySeconds: 5
  periodSeconds: 5
```

Das Ganze würde demzufolge wie folgt aussehen:

```yaml 
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-exec
spec:
  containers:
  - name: liveness
    image: registry.k8s.io/busybox
    args:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -f /tmp/healthy; sleep 600
    readinessProbe:
      exec:
      command:
      - cat
      - /tmp/healthy
    initialDelaySeconds: 5
    periodSeconds: 5
```
