# Aufgabe E - Zugriffssteuerung

## Links
- [Link zu den Ressourcen im GitLab](https://gitlab.com/ch-tbz-hf/Stud/v-cnt/-/tree/main/2_Unterrichtsressourcen/E)
- [Link zur Kubernetes-Oberfläche](https://10.5.38.10:8443/#/create?namespace=default)

## Zugriffssteuerung
MicroK8s ist von Natur aus mehrbenutzerfähig ist, was bedeutet, dass jeder Benutzer, der der microk8s-Gruppe hinzugefügt wird, Befehle gegen den MicroK8s-Cluster ausführen kann.
Allerdings kann es in bestimmten Situationen wünschenswert sein, eine gewisse Benutzerisolierung zu haben, besonders wenn mehrere Benutzer auf einen MicroK8s-Cluster zugreifen. MicroK8s ist eine vollständige Implementierung von Kubernetes, und daher können alle bestehenden Strategien zur Handhabung mehrerer Benutzer angewendet werden.

Als aller erstes, aktivieren wir RBAC mit folgendem Befehl im Terminal: ```yaml microk8s enable rbac ```
![image](https://github.com/Andreeyy/Aufgabe-B---Liveness-Readiness/assets/64062748/2c12f075-accf-4d70-8da5-c6979df86a67)

Nun erstellen wir einen Namensraum (Namespace) für einen Benutzer. Wir nehmen in diesem Fall mich und geben den Namen Andre ein. Dies machen wir mit json:
```json
{
  "apiVersion": "v1",
  "kind": "Namespace",
  "metadata": {
    "name": "alice",
    "labels": {
      "name": "alice"
    }
  }
}
```

