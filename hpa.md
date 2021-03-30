# Horizontal Pod Autoscaler

Наше видео на [Youtube](https://www.youtube.com/channel/UCqC3c7UHtwoX2wy7fdHc6gg) и новости в [Telegram](https://t.me/devops_mops)
<br><br>

Создаем Horizontal Pod Autoscaler 
```
kubectl autoscale deployment php-apache --cpu-percent=25 --min=1 --max=5
```

Устанавливаем Merics Server
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

Устанавливаем Merics Server (для KiND)

> Добавлен аргумент
>
>   --kubelet-insecure-tls

```
kubectl apply -f metrics-server.yaml
```

Проверяем, что Metrics Server запущен и собирает метрики
```
kubectl get pod -n kube-system -w |grep metrics

kubectl top pod

kubectl top node
```

Показать объекты HPA
```
kubectl get hpa -n hpa-test
```

Генерируем нагрузку на приложение
```
kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"
```

Проверяем состояние HPA и Pods
```
kubectl get hpa -n hpa-test

kubectl get pod -w
```