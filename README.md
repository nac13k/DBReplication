```SQL

```

## POSTGRES DATABASE SETUP

```SQL
CREATE TABLE GEOFENCE(
  id SERIAL PRIMARY KEY,
  device_id INT,
  provider_id INT,
  name VARCHAR(255),
  geofence_type VARCHAR(255),
  risk_zone BOOLEAN,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
CREATE TABLE DEVICE(
  id SERIAL PRIMARY KEY,
  provider_id VARCHAR(255),
  imei VARCHAR(255),
  name VARCHAR(255),
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
CREATE TABLE CURRENT_POSITION(
  id SERIAL PRIMARY KEY,
  device_id INT REFERENCES device(id),
  imei VARCHAR(255),
  provider_id VARCHAR(255),
  address VARCHAR(255),
  battery INT,
  city VARCHAR(255),
  provider_created_at TIMESTAMP,
  distance FLOAT,
  engine_status VARCHAR(255),
  event_type VARCHAR(255),
  last_connection TIMESTAMP,
  mileage FLOAT,
  orientation VARCHAR(255),
  orientation_degrees INT,
  reference VARCHAR(255),
  speed FLOAT,
  state VARCHAR(255),
  temperature INT,
  latitude FLOAT,
  longitude FLOAT,
  received_at TIMESTAMP,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
CREATE TABLE AUSER(
  id SERIAL PRIMARY KEY,
  username VARCHAR(100),
  email VARCHAR(255),
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
CREATE TABLE CHAT(
  id SERIAL PRIMARY KEY,
  provider_id VARCHAR(255),
  body VARCHAR(255),
  file_url VARCHAR(255),
  user_id INT,
  provider_created_at TIMESTAMP,
  receiver_id INT,
  user_ids VARCHAR(255),
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()  
);
CREATE TABLE ALERT(
  id SERIAL PRIMARY KEY,
  provider_id INT,
  name VARCHAR(255),
  event_type VARCHAR(255),
  category VARCHAR(50),
  provider_created_at TIMESTAMP,
  geofence_id INT,
  user_id INT,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()  
);
CREATE TABLE NOTIFICATION(
  id SERIAL PRIMARY KEY,
  provider_id VARCHAR(255),
  message VARCHAR(255),
  category VARCHAR(255),
  link VARCHAR(255),
  code VARCHAR(255),
  alert_id INT,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
CREATE TABLE CONNECTION(
	id SERIAL PRIMARY KEY,
	provider_id VARCHAR(255),
	IMEI VARCHAR(255),
	Address VARCHAR(255),
	Battery INT,
	City VARCHAR(255),
	distance FLOAT,
	engine_status VARCHAR(255),
	event_type VARCHAR(255),
	last_connection TIMESTAMP,
	mileage FLOAT,
	orientation VARCHAR(255),
	reference VARCHAR(255),
	speed FLOAT,
	state VARCHAR(255),
	temperature INT,
	latitude FLOAT,
	longitude FLOAT,
	received_at TIMESTAMP,
  device_id INT,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

## MYSQL Database Setup

```SQL
CREATE TABLE GEOFENCE(
  id INT NOT NULL AUTO INCREMENT,
  provider_id INT,
  device_id INT,
  name VARCHAR(255),
  geofence_type VARCHAR(255),
  risk_zone BOOLEAN,
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID)
);
CREATE TABLE DEVICE(
  id INT NOT NULL AUTO INCREMENT,
  provider_id VARCHAR(255),
  imei VARCHAR(255),
  name VARCHAR(255),
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID)
);
CREATE TABLE CURRENT_POSITION(
  id INT NOT NULL AUTO INCREMENT,
  device_id INT,
  provider_id VARCHAR(255),
  battery INT,
  city VARCHAR(255),
  distance FLOAT,
  engine_status VARCHAR(255),
  event_type VARCHAR(255),
  last_connection DATETIME,
  mileage FLOAT,
  orientation INT,
  reference VARCHAR(255),
  speed FLOAT,
  state VARCHAR(255),
  temperature INT,
  latitude FLOAT,
  longitude FLOAT,
  received_at DATETIME,
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID),
);
CREATE TABLE AUSER(
  id INT NOT NULL AUTO INCREMENT,
  username VARCHAR(100),
  email VARCHAR(255),
  first_name VARCHAR(100),
  last_name VARCHAR(100)  ,
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID)
);
CREATE TABLE CHAT(
  id INT NOT NULL AUTO INCREMENT,
  provider_id VARCHAR(255),
  body VARCHAR(255),
  file_url VARCHAR(255),
  RECEIVER_ID INT,
  user_ids VARCHAR(255),
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID),
);
CREATE TABLE ALERT(
  id INT NOT NULL AUTO INCREMENT,
  provider_id INT,
  name VARCHAR(255),
  event_type VARCHAR(255),
  category VARCHAR(255),
  provider_created_at DATETIME,
  geofence_id INT,
  user_id INT,
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID),
);
CREATE TABLE NOTIFICATION(
  id INT NOT NULL AUTO INCREMENT,
  provider_id VARCHAR(255),
  message VARCHAR(255),
  category VARCHAR(255),
  link VARCHAR(255),
  alert_id INT,
  code VARCHAR(255),
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID),
);
CREATE TABLE CONNECTION(
  id INT NOT NULL AUTO INCREMENT,
  provider_id VARCHAR(255),
  imei VARCHAR(255),
  address VARCHAR(255),
  battery INT,
  city VARCHAR(255),
  distance FLOAT,
  engine_status VARCHAR(100),
  event_type VARCHAR(255),
  last_connection DATETIME,
  mileage FLOAT,
  orientation VARCHAR(255),
  reference VARCHAR(255),
  speed FLOAT,
  state VARCHAR(255),
  temperature INT,
  latitude FLOAT,
  longitude FLOAT,
  received_at DATETIME,
  orientation_degrees INT,
  device_id INT,
  created_at TIMESTAMP DEFAULT current_timestamp,
  updated_at TIMESTAMP DEFAULT current_timestamp ON UPDATE current_timestamp,
  PRIMARY KEY(ID)
);
```

## SQL Server Database Setup

```SQL
CREATE TABLE GEOFENCE(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  provider_id INT,
  device_id INT,
  name VARCHAR(255),
  geofence_type VARCHAR(255),
  risk_zone BIT,
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
CREATE TABLE DEVICE(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  provider_id VARCHAR(255),
  imei VARCHAR(255),
  name VARCHAR(255),
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
CREATE TABLE CURRENT_POSITION(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  device_id INT,
  provider_id VARCHAR(255),
  battery INT,
  city VARCHAR(255),
  distance FLOAT,
  engine_status VARCHAR(255),
  event_type VARCHAR(255),
  last_connection VARCHAR(255),
  mileage FLOAT,
  orientation VARCHAR(255),
  orientation_degrees INT,
  reference VARCHAR(255),
  speed FLOAT,
  state VARCHAR(255),
  temperature INT,
  latitude FLOAT,
  longitude FLOAT,
  received_at VARCHAR(255),
  address VARCHAR(255),
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
CREATE TABLE AUSER(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  username VARCHAR(100),
  email VARCHAR(255),
  first_name VARCHAR(100),
  last_name VARCHAR(100)  ,
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
CREATE TABLE CHAT(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  provider_id VARCHAR(255),
  body VARCHAR(255),
  file_url VARCHAR(255),
  receiver_id INT,
  user_ids VARCHAR(255),
  provider_created_at DATETIME,
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
CREATE TABLE ALERT(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  provider_id INT,
  name VARCHAR(255),
  event_type VARCHAR(255),
  category VARCHAR(255),
  provider_created_at VARCHAR(255),
  geofence_id INT,
  user_id INT,
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
CREATE TABLE NOTIFICATION(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  provider_id VARCHAR(255),
  message VARCHAR(255),
  category VARCHAR(255),
  link VARCHAR(255),
  alert_id INT,
  code VARCHAR(255),
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
CREATE TABLE CONNECTION(
  id INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
  provider_id VARCHAR(255),
  imei VARCHAR(255),
  address VARCHAR(255),
  battery INT,
  city VARCHAR(255),
  distance FLOAT,
  engine_status VARCHAR(100),
  event_type VARCHAR(255),
  last_connection DATETIME,
  mileage FLOAT,
  orientation VARCHAR(255),
  reference VARCHAR(255),
  speed FLOAT,
  state VARCHAR(255),
  temperature INT,
  latitude FLOAT,
  longitude FLOAT,
  received_at DATETIME,
  orientation_degrees INT,
  device_id INT,
  created_at DATETIME NOT NULL DEFAULT(GETDATE()),
  updated_at DATETIME NOT NULL DEFAULT(GETDATE())
);
```


## Installation Batch file

### Usage

Make a folder called Dumax in Autorooter media. Make sure proper ARCH are
chosen for both NSSM and Golang compilation. [32 / 64]

Service will be created and will be persisted even after reboot. Uninstalling
the service would require to delete the Service from service list.

```BASH
[AutoRun]
XCOPY Dumax "C:\Program Files\Dumax"
CD "C:\Program Files\Dumax"
nssm install DUMAXCON dumax.exe
nssm set DUMAXCON AppDirectory "C:\Program Files\Dumax"
nssm set DUMAXCON DisplayNmae Dumax
nssm set DUMAXCON Description Dumax - Connection Storage
nssm set DUMAXCON Start SERVICE_AUTO_START
nssm set DUMAXCON ObjectName LocalSystem
nssm set DUMAXCON Type SERVICE_WIN32_OWN_PROCESS
nssm set DUMAXCON AppExit Default Restart
nssm set DUMAXCON AppRestartDelay 0
nssm set DUMAXCON AppStdout "C:\Program Files\Dumax\service.log"
nssm set DUMAXCON AppStderr "C:\Program Files\Dumax\service.log"
````

### Uninstall Batch File
```
[AutoRun]
nssm stop DUMAXCON
nssm remove DUMAXCON confirm
RMDIR /S /Q "C:\Program Files\Dumax"
```

## User Manual

### Zip

1. Descargar el archivo comprimido Dumax.zip
2. Descomprimir el archivo en una carpeta de fácil acceso
3. Asegúrese de tener el archivo install.bat y la carpeta Dumax

### USB
1. Insertar el USB
2. Asegurárse de que el mismo contenga el archivo install.bat y la carpeta Dumax


### Continuación (Ambos)
1. Editar el archivo de configuración (config.xml) con la siguiente información
   - En DBProvider seleccione su proveedor de Base de Datos de acuerdo a lo siguiente

     MySQL Server: ```<DBProvider>mssql</DBProvider>```

     SQLite: ```<DBProvider>sqlite3</DBProvider>```

     MySQL: ```<DBProvider>mysql</DBProvider>```

     Postgres: ```<DBProvider>postgres</DBProvider>```

2. Cree la Base de Datos a utilizar si no ha sido creada previamente e inserte su nombre en la etiqueta ```<Schema></Schema>``` del archivo XML

    ```XML
    <Schema>SchemaName</Schema>
    ```

3. Assegúrese de crear la base de datos con los Statements apropiados mencionados al principio del documento. Además agregue el formato que utiliza para guardar el tiempo en su sistema (US / MX) en la etiqueta ```<DbTimeZoneFormat></DbTimeZoneFormat>```.
4. Inserte su nombre de usuario y password de la base de datos.
5. Si la Base de Datos se encuentra en la misma máquina en donde el servicio será instalado continúe al paso 7.
6. Otorgue permiso de acceso remoto al Usuario de la Base de Datos de acuerdo a su proveedor. Este paso no es necesario en caso de estar utilizando SQLite.
   - Si utiliza MYSQL

             GRANT ALL PRIVILEGES
             ON database.*
             TO 'user'@'[ip destino]'
             IDENTIFIED BY 'newpassword';

   - Si utiliza SQL Server: En SQL Server Manager, de click izquierdo a la base de datos a utilizar. En el panel de *connections*, asegúrese de que la opción "Allow Remote Connections in this server" esté seleccionada.
   - Si utiliza PostgreSQL: Vaya al archivo de configuración ``` C:\Program Files\PostgreSQL\<version>\data\pg_hba.conf```  y agregue la línea
              host 		all 		all 		0.0.0.0/0 		md5
   - Asegúrese de que el archivo postgresql.conf esté escuchando a la IP asignada a su computadora

                 listen_address='*'

7. Puede configurar los nombres de los eventos en la etiqueta ``` <EventTypesNames>``` si así lo desea.
8. Finalmente, configure el usuario en la etiqueta ``` <WebUser>```  así como su contraseña

    ```XML
     <WebUser>username</WebUser>
     <Password>password</Password>
    ```

9. Asegúrese de que su Usuario de Windows tenga permisos de Administrador sobre el sistema local y no exista ningún Firewall que esté bloqueando el accesso de conexión a la Base de Datos de su Dominio (o sistema local).
10. De click derecho sobre el archivo AutoRun y seleccione la opción "Run as Administrator"

# Web Service

Please set the ```Mode``` type in the configuration file to 0.
Additional fields are required; including:

```XML
<API>
	<Client>
		<Company>Compnay Name</Company>
		<WebData> <!-- Where user data will be posted -->
			<Username>BasicAuthUsername</Username>
			<Password>BasicAuthPassword</Password>
		</WebData>
	</Client>
</API>
<TimeZone> <!-- Time Zone format for API mode -->
  <Name>America/Monterrey</Name>
  <CustomTimeDiff>-00h00m00s</CustomTimeDiff> <!-- Time difference for syncrhonization -->
</TimeZone>
```

Note that the CustomTimeDiff is only used when the customer's Clocks are not syncrhonized with the Universal Clocks.

# Significados de los Campos de la Tabla de Conexiones

| Campo | Significado | Tipo |
|:-----:|:----------:|:----:|
| ID | El ID consecutivo de almacenamiento de la base de datos | Entero |
| connection_id | El ID como está almacenado en la Base de Datos del Proveedor. | Varchar / String |
| imei | IMEI del equipo. | Varchar / String |
| address | Dirección o ubicación. | Varchar / String |
| battery | Nivel de batería del equipo. | Entero. |
| city | Ciudad donde se encuentra ubicado el equpo. | Varchar / String |
| created_at | Fecha de creación en la base de datos del proveedor | TimeStamp |
| distance | Distancia a la que se encuentra del punto de referencia | Entero |
| engine_status | Estado del motor (ver segunda tabla) | Varchar / String |
| last_connection | Fecha de la última conexión recibida | DateTime |
| mileage | Kilometraje del vehículo | Entero |
| orientation | Orientación, en grados, indicando la orientación a la que se mueve el vehículo | Entero |
| reference | Un lugar o punto de referencia en el que se encuentra el equpo | Varchar / String |
| speed | Velocidad a la que viaja el vehículo | Kilómetros / Hora |
| state | Estado en el que se encuentra el equipo | Varchar / String |
| tempetature | A la que se encuentra el equipo en Grados Celcius | Entero |
| latitude | Coordenadas, componente longitud | Flotante |
| longitude | Coordenadas, componente latitud | Flotante |
| received_at | Fecha de recibido en el servicio de replicación | DateTime |

# Significado de los Tipos de Eventos

| ID | Nombre |
|:--:|:------:|
| 1 | speed_alert | Alerta de Velocidad |
| 2 | unauthorized_movement | Movimiento no autorizado |
| 3 | engine_on | Motor encendido detectado |
| 4 | engine_off | Motor apagado detectado |
| 5 | panic | Pánico |
| 6 | position | Reporte de Posición |
| 7 | hook | Enganche |
| 8 | release | Desenganche |
| 9 | low_battery | Batería Baja |
| 10 | init_charge | Comienzo de Carga de Batería |
| 11 | end_charge | Finalización de Carga de Batería |
| 12 | poleo | Poleo |
| 13 | call_poleo | Llamado a Poleo |
| 14 | door_open | Puerta Abierta |
| 15 | door_close | Puerta Cerrada |
| 16 | engine_stop_active | Motor detenido activado |
| 17 | engine_stop_deactivated | Motoro detenido desactivado  |
| 18 | power_disconnection | Desconexión de Poder |
| 19 | power_connection | Conexión a Poder |
| 20 | temperature | Reporte de temperatura |
| 21 | gas | Reporte de gas / gasolina |
| 22 | device_off | Equipo Apagado |
| 23 | zone_in | Entrada a geocerca |
| 24 | zone_out | Salida de geocerca |
| 25 | turn | Vuelta |
| 26 | on_motion | En movimiento |
| 27 | off_motion | Detenido |
| 28 | ralenti | Ralenti |
| 29 | backup_energy_position | En modo de batería de respaldo |
| 30 | periodic_reset | Reset periódico |
| 31 | unhook | Desenganche |
| 32 | magnetic_lock_open | Puerta magnética abierta |
| 33 | magnetic_lock_close | Puerta magnética cerrada |
| 34 | acceleration | Aceleración |
| 35 | braking | Frenado |

# Del Real Custom Create Database Query [This is just for information, will be outdated after update].

```SQL
CREATE TABLE CONNECTION(
	id int NOT NULL IDENTITY(1,1),
	connection_id varchar(255),
  name varchar(255),
	IMEI varchar(255),
	Address varchar(255),
	Battery INT,
	City varchar(255),
	created_at datetime,
	distance float,
	engine_status varchar(255),
	event_type varchar(255),
	last_connection datetime,
	mileage float,
	orientation varchar(255),
	reference varchar(255),
	speed int,
	state varchar(255),
	temperature int,
	latitude float,
	longitude float,
	received_at datetime,
	PRIMARY KEY (ID)
);
```

# To run in client's database (****)

```SQL
ALTER TABLE connection ADD orientation_degrees int;
ALTER TABLE connection
  ALTER COLUMN orientation varchar(255);
ALTER TABLE connection
  ALTER COLUMN speed float;
```

# Considerations

Please tell the Administrators if you are:

- MS SQL Server without MX Date format
- Any other database without US / International Date Format

# Versioning:

- **1.0**: Estable.
  - Inicio de proyecto y petición de conexiones en modo replica.
  - Primer aplicación installada a Motum
- **1.1**: Estable + Windows SQL Server 2014
  - Configuración Dinámica XML para Web Service o Modo API
  - Queries específicos para SQL Server en Español (México)
  - Tipos de Evento dinámicos
  - Contiene API init, pero no funcional.
  - Segunda versión instalada a Motum.
- **i.1.1**: API versión estable (sólo tabla de conexiones)
  - Instalación hecha a motum.
- *Beta*: Actual. WIP.
  - Modificación XML extendida
  - Campos editados para ser aceptada por endpoints.
  - Actualmente en [#]oh_api_sql_v2.delta


# Updates

* Error con respecto al recibo de notificationes, se editó MapAPI para que de nuevo comenzara a enviar el ```Device``` y el ```Usuario``` en la respuesta desde el endpoint.
* Reemplazar ```device.Insert()``` por ```device.InsertIfNotExists()``` en todas las instancias de Replica Mode; para evitar cualquier probabilidad de que se tome esta ruta. 

