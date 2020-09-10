# k8s-crd-demo

## Usage:

- install crd
``` bash
make install
```
- run local
```bash
make run
```
- create sample job
```bash
kubectl apply -f config/samples/batch_v1_cronjob.yaml
```

```yaml
apiVersion: batch.dashuai.io/v1
kind: CronJob
metadata:
  name: cronjob-sample
spec:
  schedule: "*/1 * * * *"
  startingDeadlineSeconds: 60
  concurrencyPolicy: Allow
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: hello
              image: busybox
              args:
                - /bin/sh
                - -c
                - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```
- build image
```
make docker-build docker-push
```
- deploy to cluster
```bash
make deploy
```
