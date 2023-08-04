## Why?

 - With kube-green, you'll have environmentally friendly development practices through reduced energy consumption. Additionally, you'll effectively trim resource costs:

   - Are your development pods consistently active over weekends or during nighttime? This not only leads to unnecessary resource consumption but also incurs additional costs.

   - Have you ever wondered about the annual CO2 emissions attributed to a single pod? According to [kube-green's estimations](https://kube-green.dev/docs/getting-started/), each pod contributes approximately 11 kg of CO2 equivalent per year.

## How to install it?

1. Install a kubernetes cluster in your local machine:

```kind create cluster --name kube-green```

2. Install the cert-manager

```kubectl apply -f https://github.com/jetstack/cert-manager/releases/latest/download/cert-manager.yaml```

3. Install kube-green

```kubectl apply -f https://github.com/kube-green/kube-green/releases/latest/download/kube-green.yaml```


## How to test it?

1. Create 6 PODs using deployments 

```
kubectl create ns test-sleep
kubectl -n test-sleep create deploy nginx-1 --image=nginx --replicas=5


## do-not-sleep-nginx pods will not be affected by kube-green
kubectl -n test-sleep create deploy do-not-sleep-nginx --image=nginx --replicas=2


kubectl -n test-sleep create deploy nginx-2 --image=nginx --replicas=2
```

2. Choose one of the options below for testing:

2.1. Create a SleepInfo based on minutes

- sleep every 1st minute and wake up every 5th minute

```kubectl apply -f sleep-info-minutes.yaml```

2.2. Create a SleepInfo based on fixed interval

- Set to sleep at 18:00 and wake up at 08:00 on weekdays.

```kubectl apply -f sleep-info-fixed-interval.yaml```

### Resources

- https://kube-green.dev/ 