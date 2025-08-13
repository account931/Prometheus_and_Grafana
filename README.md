
<p>Both prometheus and grafana  </p>

<code>docker compose up -d </code>  OR <code> docker-compose up -d </code>

Access Prometheus: http://localhost:9090  </br>  UI => http://localhost:9090/targets

Access Grafana: http://localhost:3000 (default login: admin / admin)

</br></br>

Connect Grafana to Laravel Filament sql container and set Grafana datasource, create one network 'filament-net':
<code> docker network connect filament-net grafana  </code>
<code> docker network connect filament-net my_filament_laravel_12-mysql-1 </code>
Grafana datasource set up:  Host:	my_filament_laravel_12-mysql-1:3306


Connect Prometheus and Laravel to same network filament-net'
docker network connect filament-net my_filament_laravel_12-laravel.test-1
docker network connect filament-net prometheus

Then in prometheus.yml =>  targets: ['laravel-container-name:8000']

Grafana datasource set up:  Prometheus server URL :	http://prometheus:9090





Command to enter Grafana container:   <code> docker exec -it grafana sh </code>  </br>

Command to enter Filament sql container: <code> docker exec -it my_filament_laravel_12-mysql-1 bash </code>

<p> ----------------------------------------------------------------------------------------- </p>

## 103. Screenshots
![Screenshot](screenshots/grafana.png)  </br>