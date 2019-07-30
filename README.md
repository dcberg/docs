# Documentation for the Voyager project

## [Deploy the DB2 service](DB2.md)

## [Deploy the MQ service](MQ.md)

## Deploy the portfolio service:
1. create required secret

```
$ kubectl create secret generic jwt -n stock-trader --from-literal=audience=stock-trader --from-literal=issuer=http://stock-trader.ibm.com
```

2. build the image

```
$ git clone https://github.com/thevoyagerproject/portfolio.git
$ cd portfolio/manifests
$ kubectl apply -f deploy.yaml -n stock-trader

# validate pod has reached running status
$ kubectl get pods -n stock-trader

# view logs to validate no errors
$ kubectl logs -c portfolio --namespace=stock-trader --selector="app=portfolio,solution=stock-trader"
```

## Deploy the trader service:

```
$ git clone https://github.com/thevoyagerproject/trader.git
$ cd trader/manifests
$ kubectl apply -f deploy.yaml -n stock-trader
```

## Deploy the stock-quote service:

```
$ git clone https://github.com/thevoyagerproject/stock-quote.git
$ kubectl apply -f stock-quote/manifests/deploy.yaml -n stock-trader
```

## Deploy the loyalty service:

```
$ git clone https://github.com/thevoyagerproject/loyalty-level.git
$ kubectl apply -f loyalty-level/manifests/deploy.yaml -n stock-trader
```

