# Horizontal Pod Autoscaler

Um einen Horizontal Pod Autoscaler zu erstellen, musste von uns zuerst einige Theorie aufgenommen werden, um das Ganze zu verstehen. Ein HorizontalPodAutoscaler ist ein Mechanismus in Kubernetes, der automatisch eine Arbeitslastsressource aktualisiert. 
Das Hauptziel besteht darin, die Arbeitslast automatisch zu skalieren, um der Nachfrage gerecht zu werden. Horizontales Skalieren bedeutet, dass die Reaktion auf eine erhöhte Last darin besteht, mehr Pods bereitzustellen. 
Dies bedeutet, zusätzliche Pods für die Arbeitslast zu starten. Im Gegensatz dazu bezieht sich vertikales Skalieren darauf, bereits laufenden Pods mehr Ressourcen zuzuweisen. Wir konzentrieren uns in dieser Aufgabe C jedoch auf das horizontale Skalieren.
Der HorizontalPodAutoscaler überwacht die aktuelle Auslastung der Pods. Wenn die Last zunimmt und die Anzahl der Pods unterhalb des konfigurierten Maximums liegt, skaliert der HPA automatisch hoch, indem er mehr Pods für die Arbeitslast startet. 
Wenn die Last abnimmt und die Anzahl der Pods über dem konfigurierten Minimum liegt, skaliert der HPA die Arbeitslast automatisch herunter, um Ressourcen zu sparen.
Wie wir dies verstanden haben, bietet der HorizontalPodAutoscaler zusammengefasst, eine Möglichkeit, die Ressourcennutzung in Kubernetes automatisch an die dynamischen Anforderungen einer Anwendung anzupassen.

Damit wir ein Beispiel des HPA in dieser Aufgabe auzeigen können, brauchen wir zuerst ein Deployment, das einen Container mit dem Image "hpa-example" ausführt und es als Service freigibt. Dafür verwenden wir diesen Manifest in unserem Kubernetes Dashboard:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-apache
spec:
  selector:
    matchLabels:
      run: php-apache
  template:
    metadata:
      labels:
        run: php-apache
    spec:
      containers:
      - name: php-apache
        image: registry.k8s.io/hpa-example
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
          requests:
            cpu: 200m
---
apiVersion: v1
kind: Service
metadata:
  name: php-apache
  labels:
    run: php-apache
spec:
  ports:
  - port: 80
  selector:
    run: php-apache
```

Wir sehen sofort, wie es das Deployment erstellt hat:
![image](https://github.com/Andreeyy/Aufgabe-B---Liveness-Readiness/assets/64062748/806764c2-7ab3-44d3-95e7-f09b511760f3)

Den Pod:
![image](https://github.com/Andreeyy/Aufgabe-B---Liveness-Readiness/assets/64062748/51be115a-817b-4d57-9c03-1ded435d3c81)

Und auch den Service:
![image](https://github.com/Andreeyy/Aufgabe-B---Liveness-Readiness/assets/64062748/1cc5c1f5-63aa-4437-8c4a-2e790e2f470c)




