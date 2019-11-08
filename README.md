# Start with nginx loadbalancer

— Go to the directory ***nginx-loadbalacer*** <br>
— Open file ***nginx-loadbalacer/nginx/nginx.conf*** <br> 
— Find part of code like this: <br>
  
```
upstream app_servers {

        server nginx-loadbalacer_your_server_1:5000;
	server nginx-loadbalacer_your_server_2:5000;
	server nginx-loadbalacer_your_server_3:5000;
	
    }
```
— This variant for **scale=3**. If you need more servers, change the string
```
server nginx-loadbalacer_your_server_(number):5000;
```
— where **(number)** — the required number of servers<br>
— After that go to ***nginx-loadbalacer*** and change file ***docker-compose.yml***. Find the part of code:
```
your_server:
  build: hits
  depends_on:
   - redis
  networks:
   - public
   - secret
  volumes:
   - logs:/flask/logs
  deploy:
   mode: replicated
   replicas: 3
```
— where replicas: **(number)** — the required number of servers.<br>
— Start servers for help command:
```
docker-compose --compatibility up --build -d
```

# Start with traefik loadbalancer

— Go to the directory ***traefik-loadbalancer*** <br>
— Open file ***docker-compose.yml*** <br> 
— Find part of code like this: <br>
  
```
hits:
  build: .
  image: hits:compose
  labels:
   - "traefik.frontend.rule=HostRegexp:{catchall:.*}"
  depends_on:
   - redis
  networks:
   - public
   - secret
  volumes:
   - logs:/flask/logs
  deploy:
   mode: replicated
   replicas: 3
```
— where replicas: **(number)** — the required number of servers.<br>
— Start servers for help command:
```
docker-compose --compatibility up --build -d
```
