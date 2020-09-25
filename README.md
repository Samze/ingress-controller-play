### Ingress playtimes

1. Run install_istio.sh
1. kubectl apply -f .
1. kubectl port-forward -n istio-system svc/istio-ingressgateway 9000:80
1. kubectl port-forward -n ingress-nginx svc/ingress-nginx-controller 9001:80
1. kubectl port-forward -n projectcontour svc/envoy 9002:80

1. curl -H "Host: example.com" localhost:9000 # test istio
1. curl -H "Host: example.com" localhost:9001 # test nginx
1. curl -H "Host: example.com" localhost:9002 # test contour

1. curl -H "Host: example.com" localhost:9000/static/css/styles.css # test istio
1. curl -H "Host: example.com" localhost:9001/static/css/styles.css # test nginx
1. curl -H "Host: example.com" localhost:9002/static/css/styles.css # test
   contour
