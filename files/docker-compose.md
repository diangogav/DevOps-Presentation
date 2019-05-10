<h4 style="text-transform: none;"> Docker Compose</h4>

```Groovy
version: "3.2"

services:
  web:
    deploy:
      replicas: 1
    image: //URL imagen Docker
    ports:
      - "80:80"
  wfc:
    deploy:
      replicas: 1
    image: //URL imagen Docker
    ports:
      - "83:83"
```