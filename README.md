### Ingress playtimes

Install ingress controllers istio/contour/nginx
1. Run install_istio.sh
1. kubectl apply -f .

Port forward their internal services
1. kubectl port-forward -n istio-system svc/istio-ingressgateway 9000:80
1. kubectl port-forward -n ingress-nginx svc/ingress-nginx-controller 9001:80
1. kubectl port-forward -n projectcontour svc/envoy 9002:80

Test root paths
* curl -H "Host: example.com" localhost:9000 # test istio
* curl -H "Host: example.com" localhost:9001 # test nginx
* curl -H "Host: example.com" localhost:9002 # test contour

Test subpaths
* curl -H "Host: example.com" localhost:9000/static/css/styles.css # test istio
* curl -H "Host: example.com" localhost:9001/static/css/styles.css # test nginx
* curl -H "Host: example.com" localhost:9002/static/css/styles.css # test contour

---
Differences in how each ingress-controller hadnles "path".

* Doing a subdomain  `curl -H "Host: example.com" localhost:900x/static/css/styles.css -i`

| Path  | /  |  /* | /.+ |  
|---|---|---|---|
| istio |  ❌ | ✅   |  ❌| 
| nginx |  ✅  |  ✅  |   ❌ | 
| contour |  ✅ | ❌   | ✅ | 

