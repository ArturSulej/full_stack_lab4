# full_stack_lab4
Rozwiązanie zadań dla laboratorium4 z przedmiotu Programowanie Full Stack w Chmurze Obliczeniowej

## Przygotowanie środowiska przed użyciem plików

1. Upewnić się, że minikube jest uruchomiony: ```minikube start```
2. Utworzyć przestrzeń nazw lab4: ```kubectl create namespace lab4```

## Zadanie 1
1. Wykorzystać plik _lab4-pod.yaml_ w przestrzeni nazw lab4: `kubectl apply -f lab4-pod.yaml`
2. Poprawność utworzenia podów można sprawdzić za pomocą poleceń: <br>
`kubectl get pods -n lab4` <br>
`kubectl describe pods -n lab4` <- Wyświetlenie poprawności skonfigurowania zasobów <br>
`kubectl top pod -n lab4` <- monitorowanie wykorzystania zasobów <br>

## Zadanie 2
1. Wykorzystać plik _restrictednginx-deployment.yaml_: ```kubectl apply -f restrictednginx-deployment.yaml```
2. Poprawność utworzenia można sprawdzić za pomocą poleceń: <br>
```kubectl get deployment restrictednginx -n lab4``` < - Należy upewnić się, że pole AVAILABLE wskazuje, że wszystkie 3 repliki są gotowe <br>
```kubectl get pods -n lab4``` <-  potwierdzienie utworzenia podów <br>

# Alternatywna metoda - bez plików
Poniższa metoda pozwala na wykonanie zadań bez konieczności używania plików .yaml
## Przygotowanie środowiska przed użyciem plików

1. Upewnić się, że minikube jest uruchomiony: ```minikube start```
2. Utworzyć przestrzeń nazw lab4: ```kubectl create namespace lab4```

### Utworzenie quota
Quota pozwala na zarządzanie zasobami w odniesieniu do przestrzeni nazw. W tym przypadku pozwala na wykonanie zadania1. <br>
`kubectl create quota lab4-quota --namespace=lab4 --hard=limits.cpu=1000m,limits.memory=1Gi,pods=5`

### Uruchomienie Deployment
`kubectl create deploy restrictednginx --image=nginx -n lab4 --replicas=3`

### Ustawienie parametrów dla Deployment
`kubectl set resources deployment restrictednginx -n lab4 --requests=memory=64Mi,cpu=125m --limits=memory=256Mi,cpu=250m`
