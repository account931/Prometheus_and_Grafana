
Both prometheus and grafana  </br>

<code>docker-compose up -d </code>  OR <code> docker-compose up -d </code>

Access Prometheus: http://localhost:9090
Access Grafana: http://localhost:3000 (default login: admin / admin)

</br></br>

Connect Grafana to filament sql container and set Grafana datasource:
<code> docker network connect filament-net grafana  </code>
<code> docker network connect filament-net my_filament_laravel_12-mysql-1 </code>


Grafana datasource set up:  Host:	my_filament_laravel_12-mysql-1:3306


Command to enter Grafana container:   <code> docker exec -it grafana sh </code>  </br>

Command to enter Filament sql container: <code> docker exec -it my_filament_laravel_12-mysql-1 bash </code>

