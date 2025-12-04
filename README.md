
<p> Both prometheus and grafana  </p>

<code> docker compose up -d </code>  OR <code> docker-compose up -d </code>

Access Prometheus: http://localhost:9090  OR  UI => http://localhost:9090/targets  </br>

Access Grafana: http://localhost:3000 (default login: admin / admin)                   </br>

</br></br>

<p> How connect Grafana and Prometheus to my_filament_laravel_12 (need to run every time). Variant 1. Spoiler: use Variant 2 </p>
Connect Grafana to Laravel Filament sql container and set Grafana datasource, create one network 'filament-net':
<code> docker network connect filament-net grafana  </code>
<code> docker network connect filament-net my_filament_laravel_12-mysql-1 </code>
Grafana SQL datasource set up for SQL:  Host:	my_filament_laravel_12-mysql-1:3306  

</br></br>

------------------------------------------------




------------------------------------------------

</br>
<p> Connect SQL dataset </p></br>
Configure new Data source for SQL </br>
Host URL: my_filament_laravel_12-mysql-1:3306
Database name: laravel_filament


------------------------------------------------


</br>
<p> How connect Grafana/Prometheus and Laravel. Variant 2, USE IT!!! : </p>   since 'sail' network is already created by Laravel-filament_12  
</br>
Install plugin Prometheus</br>
Prometheus server URL:  http://prometheus:9090
You still need to manually connect containers (docker network connect) because the containers are not started from the same docker-compose.yml file, so Docker doesn't automatically attach them to shared networks unless explicitly declared and correctly named.

<code>
docker network connect sail my_filament_laravel_12-mysql-1               
docker network connect sail my_filament_laravel_12-laravel.test-1        
</code>


</br>

Connect Prometheus and Laravel to same network 'filament-net'.              </br>
docker network connect filament-net my_filament_laravel_12-laravel.test-1   </br>
docker network connect filament-net prometheus                              </br>
Then in prometheus.yml =>  targets: ['laravel-container-name:8000']         </br>
Grafana Prometheus datasource set up:  Prometheus server URL :	http://prometheus:9090  </br>

</br></br>
------------------------------------------------






</br>
<p> Connect Infinity dataset </p></br>
Install plugin yesoreyeram-infinity </br>
Go inside Filament Laravel container and run =>    php artisan serve --host=0.0.0.0 --port=8000  </br>
Now can use Docker open URL =>  http://my_filament_laravel_12-laravel.test-1:8000/api/owners        </br>
In Parsing options =>  in Rows/Root set =>  $.data </br>

2. Way to query Sanctum protected Api route: </br>
 generate token in tinker or console or anywhere else -> go to Data Source (cant configure for Panel only, but for all Data source) -> Auth -> Bearer token -> insert token. You might additionally need to go to => Security => and add to 'Allowed hosts' your 'http://my_filament_laravel_12-laravel'.test-1:8000

</br>

------------------------------------------------

</br>
<p> Connect BigQuery dataset </p></br>
Install new connection: 'Google BigQuery' -> config new datasource 'Google BigQuery'  -> add JWT file (it will load 'Project ID', 'Token URI') -> click 'Save and test'

Make sure to enable 'Cloud Resource Manager API'  in https://console.cloud.google.com/apis/library/cloudresourcemanager.googleapis.com

# BigQuery query example, top 2 most viwed, use Bar chart and set x-axis as total_views
 SELECT 
 product_id, 
 COUNT(product_id) AS total_views 
 FROM analytics_dataset.product_views  #datasetName.tableName
 GROUP BY product_id 
 ORDER BY total_views DESC 
 LIMIT 2

 
------------------------------------------------

</br></br>


Command to enter Grafana container:   <code> docker exec -it grafana sh </code>  </br>

Command to enter Filament sql container: <code> docker exec -it my_filament_laravel_12-mysql-1 bash </code>

<p> ----------------------------------------------------------------------------------------- </p>

## 103. Screenshots
![Screenshot](screenshots/grafana.png)  </br>
![Screenshot](screenshots/grafana2.png)  </br>
![Screenshot](screenshots/grafana3.png)  </br>
![Screenshot](screenshots/grafana4.png)  </br>