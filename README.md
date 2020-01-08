# UAS Teknologi Cloud

#### Nama : Siska Rahmawati
#### NIM : 185410089
#### Kelas : TI-9


## Membuat Image
Membuat sebuah image menggunakan Python Flask dengan nama
`siskara/my-app:v1`
- Dockerfile
```dockerfile
FROM python:2.7
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]

```
- app.py
```python
# app.py - a minimal flask api using flask_restful
from flask import Flask
from flask_restful import Resource, Api

app = Flask(__name__)
api = Api(app)

class HelloWorld(Resource):
    def get(self):
        return {'nama': 'halo'}

api.add_resource(HelloWorld, '/')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')

```
- requirements.txt
```
flask
flask_restful
```

## Menjalankan di Kubernetes
1. Membuat deployment untuk image hehe-flask
```bash
$ kubectl create deployment my-app --image=siskara/my-app:v1
deployment.apps/my-app created
```
2. Membuat service untuk meng-expose port 5000 image my-app
```bash
$ kubectl expose deployment my-app --type=LoadBalancer --port=5000
service/my-app exposed
```
3.  Melihat Service yang berjalan
```bash
$ kubectl get services
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
my-app   	LoadBalancer   10.96.182.145  <pending>     5000:31624/TCP   12s
kubernetes   ClusterIP      10.96.0.1      <none>        443/TCP          5m36s
```
4. Terlihat bahwa port 5000 di expose ke port 31624
```bash
$ kubectl get services
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
my-app   	LoadBalancer   10.96.182.145  <pending>     5000:31624/TCP   12s
kubernetes   ClusterIP      10.96.0.1      <none>        443/TCP          5m36s
```
5. Jalankan melalui browser



