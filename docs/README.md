## Kong Ingress Controller (KIC) কী?

Kong Ingress Controller (KIC) হলো Kubernetes-এর জন্য একটি ওপেন সোর্স Ingress Controller যা Kong Gateway-কে Kubernetes Ingress বা Gateway API রিসোর্সগুলো (যেমন Ingress, HTTPRoute) থেকে কনফিগার করে। এটি ট্রাফিক রাউটিং, লোড ব্যালান্সিং, হেলথ চেক এবং Kong-এর সব প্লাগিন (রেট লিমিটিং, অথেনটিকেশন) Kubernetes CRD-এর মাধ্যমে ম্যানেজ করে। [developer.konghq](https://developer.konghq.com/kubernetes-ingress-controller/)

## ওপেন সোর্স স্ট্যাটাস

হ্যাঁ, KIC সম্পূর্ণ ওপেন সোর্স—Apache 2.0 লাইসেন্সের অধীনে GitHub-এ উপলব্ধ এবং কোনো এন্টারপ্রাইজ লাইসেন্স ছাড়াই কোর ফিচারগুলো চালানো যায়। কিছু অ্যাডভান্সড এন্টারপ্রাইজ ফিচার (যেমন DB-less মোডে লাইসেন্স চেক) ছাড়া সবকিছু ফ্রি। [perplexity](https://www.perplexity.ai/search/771ae10a-d591-4360-979f-485a55db95d1)

## সুবিধা ও অসুবিধা

**সুবিধা:**
- Kubernetes-native API গেটওয়ে ম্যানেজমেন্ট সহ প্লাগিন সাপোর্ট (রেট লিমিট, ক্যাশিং, অথেন)।
- Gateway API-এর ১০০% কমপ্লায়েন্স এবং হাই পারফরম্যান্স (NGINX-ভিত্তিক)।
- মাল্টি-গেটওয়ে ডেপ্লয়মেন্ট এবং microservices-এর জন্য আদর্শ। [developer.konghq](https://developer.konghq.com/kubernetes-ingress-controller/)

**অসুবিধা:**
- কনফিগারেশন কমপ্লেক্স হতে পারে নতুনদের জন্য।
- ক্রস-নেমস্পেস সাপোর্ট লিমিটেড, প্রতি নেমস্পেসে আলাদা ইন্সট্যান্স লাগে।
- রিসোর্স ইনটেন্সিভ হলে স্কেলিং চ্যালেঞ্জ। [kubevious](https://kubevious.io/blog/post/comparing-top-ingress-controllers-for-kubernetes/)

## সম্পূর্ণ ওপেন সোর্স বিকল্প

- **NGINX Ingress Controller**: হাই পারফরম্যান্স L7 রাউটিং, Apache 2.0 লাইসেন্স—সিম্পল প্রক্সি হিসেবে ভালো। [blog.nginx](https://blog.nginx.org/blog/the-ingress-nginx-alternative-open-source-nginx-ingress-controller-for-the-long-term)
- **Traefik**: অটো-ডিসকভারি সহ ডায়নামিক কনফিগ, Gateway API সাপোর্ট।
- **HAProxy Ingress**: TCP/L4-এ স্ট্রং, অ্যানোটেশন-ভিত্তিক।
- **Istio Ingress Gateway**: সার্ভিস মেশ সহ অ্যাডভান্সড ট্রাফিক কন্ট্রোল। [theinfinity](https://theinfinity.dev/articles/kubernetes-ingress-gateway-comparison-traefik-istio-kong)

## অন্য টুলসের সাথে পার্থক্য

| টুল              | প্রোটোকল সাপোর্ট     | কনফিগ মেথড          | প্লাগিন/এক্সটেনশন | কমপ্লেক্সিটি |
|-------------------|-----------------------|-----------------------|---------------------|--------------|
| **Kong KIC**    | HTTP/gRPC/TCP/UDP   | CRD/Gateway API      | ১০০+ প্লাগিন      | মাঝারি-উচ্চ  [developer.konghq](https://developer.konghq.com/kubernetes-ingress-controller/) |
| **NGINX Ingress**| HTTP/gRPC/TCP       | অ্যানোটেশন/Ingress  | লিমিটেড            | নিম্ন  [blog.nginx](https://blog.nginx.org/blog/the-ingress-nginx-alternative-open-source-nginx-ingress-controller-for-the-long-term) |
| **Traefik**     | HTTP/gRPC/TCP/UDP   | অটো-ডিসকভারি/CRD    | মিডিয়াম           | নিম্ন  [theinfinity](https://theinfinity.dev/articles/kubernetes-ingress-gateway-comparison-traefik-istio-kong) |
| **Istio**       | সব                   | VirtualService/CRD   | সার্ভিস মেশ        | উচ্চ  [theinfinity](https://theinfinity.dev/articles/kubernetes-ingress-gateway-comparison-traefik-istio-kong) |

Kong প্লাগিন-ভিত্তিক এবং Gateway API-এ স্ট্রং, যেখানে NGINX সিম্পল প্রক্সি। [theinfinity](https://theinfinity.dev/articles/kubernetes-ingress-gateway-comparison-traefik-istio-kong)

## কখন, কেন, কীভাবে ব্যবহার

Kubernetes-এ microservices/API গেটওয়ে দরকার হলে যখন লোড ব্যালান্সিং, সিকিউরিটি প্লাগিন বা Gateway API লাগে—হোম ল্যাব বা প্রোডাকশনে। কীভাবে: Helm চার্ট দিয়ে ইন্সটল করে Ingress/HTTPRoute YAML অ্যাপ্লাই করুন। [developer.konghq](https://developer.konghq.com/kubernetes-ingress-controller/)

## Kong-এর অন্য ওপেন সোর্স টুলস

- **Kong Gateway**: কোর API গেটওয়ে (NGINX-ভিত্তিক), DB-less/হাইব্রিড মোডে চলে। [konghq](https://konghq.com/products/kong-gateway)
- **Kong Chartmuseum**: Helm চার্ট রিপোজিটরি।
- **Insomnia**: API টেস্টিং ক্লায়েন্ট। সব Apache 2.0। [konghq](https://konghq.com/products/kong-gateway)

## ইন্সটল ও কনফিগারেশন (k3s/k8s)

আপনার k3s/k8s রানিং হলে (যেমন আপনার হোম ল্যাব):

1. Gateway API CRD ইন্সটল: `kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.0.0/standard-install.yaml` [tech.aufomm](https://tech.aufomm.com/explore-kubernetes-gateway-api-with-kong-ingress-controller/)
2. Helm repo যোগ: `helm repo add kong https://charts.konghq.com && helm repo update`
3. KIC ইন্সটল: `helm install kong kong-ingress-controller --namespace kong --create-namespace --set gateway.provision.enabled=true --set ingressController.installCRDs=false` [perplexity](https://www.perplexity.ai/search/49e6c0c6-d87d-48f4-91fb-4e88eff1839c)
4. GatewayClass তৈরি: `kubectl apply -f https://github.com/Kong/charts/raw/master/charts/kong-ingress-controller/example/gateway-api/gatewayclass.yaml`
5. চেক: `kubectl get gatewayclass` [developer.konghq](https://developer.konghq.com/kubernetes-ingress-controller/)

## বেসিক ব্যবহার

Gateway এবং HTTPRoute YAML তৈরি করুন:
```
apiVersion: gateway.networking.k8s.io/v1beta1
kind: Gateway
metadata:
  name: kong-gateway
  namespace: default
spec:
  gatewayClassName: kong
---
apiVersion: gateway.networking.k8s.io/v1beta1
kind: HTTPRoute
metadata:
  name: http-route
spec:
  parentRefs:
  - name: kong-gateway
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /api
    backendRefs:
    - name: your-service
      port: 80
```
অ্যাপ্লাই: `kubectl apply -f route.yaml`। Kong অটো রাউট করে। রেট লিমিট যোগ: `konghq.com/rate-limiting: "5 r/s"` অ্যানোটেশন। [perplexity](https://www.perplexity.ai/search/49e6c0c6-d87d-48f4-91fb-4e88eff1839c)

## বাস্তব কাজের উদাহরণ

হোম ল্যাবে: k3s-এ Flask অ্যাপ ডেপ্লয় করুন, KIC দিয়ে `/api/users` রাউট যোগ করুন সহ অথেন (key-auth প্লাগিন) এবং Prometheus মনিটরিং। ট্রাফিক: `curl http://kong-ip/api/users -H "apikey: xxx"`—Kong চেক করে backend পাঠায়, Grafana-তে PromQL দিয়ে কোয়েরি করুন। প্রোডে: gRPC microservices-এ TCPRoute দিয়ে লোড ব্যালান্স। [developer.konghq](https://developer.konghq.com/kubernetes-ingress-controller/)

## KIC, Kong Gateway, Gateway API বিস্তারিত

**Kong Gateway**: হাই-পারফর্ম্যান্স API গেটওয়ে—রাউটিং, প্লাগিন (১০০+), L4/L7 সাপোর্ট। KIC এটাকে কনট্রোল করে। [konghq](https://konghq.com/products/kong-gateway)

**Gateway API**: Kubernetes-এর নতুন স্ট্যান্ডার্ড (Ingress-এর পরিবর্তে)—GatewayClass, Gateway, HTTPRoute/TCPRoute দিয়ে ফাইন-গ্রেইন রাউটিং। KIC এর প্রথম কমপ্লায়েন্ট। কেন: Ingress-এর লিমিট ছাড়াই মাল্টি-টেনান্ট। কখন: মাল্টি-ক্লাস্টার বা অ্যাডভান্সড রাউটিং। [tech.aufomm](https://tech.aufomm.com/explore-kubernetes-gateway-api-with-kong-ingress-controller/)

কী করা যায়: TCP/UDP রাউট (যেমন MySQL: TCPRoute), রেট লিমিট, gRPC। উদাহরণ: k3s-এ MikroTik মনিটরিং-এর মতো নেটওয়ার্ক ডিভাইস রাউট। ধাপে ধাপে উপরে দেওয়া। [perplexity](https://www.perplexity.ai/search/49e6c0c6-d87d-48f4-91fb-4e88eff1839c)