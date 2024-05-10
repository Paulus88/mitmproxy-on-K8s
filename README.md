# Deploy mitmproxy + mitmweb on Kubernetes
This is a basic deployment to run mitmproxy and mitmweb using the Docker Hub container:
https://hub.docker.com/r/mitmproxy/mitmproxy

As I was unable to find this I decided to create my own manifest and share it with everyone.

Simply does the same as instructed on Docker Hub but as a Kubernetes Deployment manifest.

The manifest simply deploys the latest DEV version of mitmproxy and mitmweb directly to the your host network and listens on *. mitmproxy normally will run on port 8080 and mitmweb 8081.
## Deployment
```
kubectl apply -f https://raw.githubusercontent.com/Paulus88/mitmproxy-on-K8s/main/mitmproxy.yml
```
## Additional features you could consider
Changing the arguments to run mitmdump, or change any settings:
```
      - args:
        - mitmweb
        - --web-host
        - "*"
        - --no-web-open-browser
```
Manifest includes readinessProbe and livenessProbe that monitors mitmweb port 8081, keep this in mind if your changing settings.

I recommend adding a **persisted volume** for the CA certificate, as mentioned on Docker Hub. Mount: /home/mitmproxy/.mitmproxy

## All Credit to
https://mitmproxy.org/
For all their hard work!
