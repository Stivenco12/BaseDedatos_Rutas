# BaseDedatos_Rutas

CREATE DATABASE Rutass;

USE Rutass;

CREATE TABLE Conductor(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Telefono VARCHAR(30),
  Cedula VARCHAR(30)
);


CREATE TABLE Vehiculo(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Placa VARCHAR(30),
  Capacidad Decimal(10,2),
  Tipo VARCHAR(60)
);

CREATE TABLE Ruta(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Descricion VARCHAR(120),
  IdVehiculo_fk INT,
  CONSTRAINT Fk_VehiculoRuta FOREIGN KEY (IdVehiculo_fk) REFERENCES Vehiculo(id),
  IdCoductor_fk INT,
  CONSTRAINT FK_ConductorRuta FOREIGN KEY (IdCoductor_fk) REFERENCES Conductor(Id)
);


CREATE TABLE Auxiliar(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Telefono VARCHAR(13),
  Cedula VARCHAR(20)
);


CREATE TABLE Cliente(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Correo VARCHAR(50),
  Telefono VARCHAR(20),
  Direccion VARCHAR(40),
  Cedula VARCHAR(50)
);

CREATE TABLE Pais(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50)
);

CREATE TABLE Ciudad(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Idpais_fk INT,
  CONSTRAINT Fk_PaisCiudad FOREIGN KEY (Idpais_fk) REFERENCES Pais(Id)
);


CREATE TABLE Sucursal(
  Nombre VARCHAR(50),
  Direccion VARCHAR(30),
  IdCiudad_fk INT,
  CONSTRAINT Fk_CiudadSucurlsal FOREIGN KEY (IdCiudad_fk) REFERENCES Ciudad(Id)
);

CREATE TABLE Paquete(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Numero VARCHAR(50),
  Peso DECIMAL(10,2),
  Dimenciones VARCHAR(50),
  Contenido VARCHAR(100),
  Valor DECIMAL(10,2)
);

CREATE TABLE Evento(
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  Ubicacion VARCHAR(40),
  Estado VARCHAR(60),
  IdPaquete_fk INT,
  CONSTRAINT FK_PaqueteEvento FOREIGN KEY (IdPaquete_fk) REFERENCES Paquete(id)
);

ALTER TABLE Sucursal
ADD Id INT AUTO_INCREMENT PRIMARY KEY;

CREATE TABLE Envio (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  Estado VARCHAR(59),
  IdCliente_fk INT,
  CONSTRAINT FK_ClienteEnvio FOREIGN KEY (IdCliente_fk) REFERENCES Cliente(Id),
  IdPaquete_fk INT,
  CONSTRAINT FK_PaquetesEvento FOREIGN KEY (IdPaquete_fk) REFERENCES Paquete(Id),
  IdRuta_fk INT,
  CONSTRAINT FK_RutaEvento FOREIGN KEY (IdRuta_fk) REFERENCES Ruta(Id),
  IdSucursal_fk INT,
  CONSTRAINT FK_SucursalEvento FOREIGN KEY (IdSucursal_fk) REFERENCES Sucursal(Id),
  IdAuxiliar_fk INT,
  CONSTRAINT FK_AuxiliarEvento FOREIGN KEY (IdAuxiliar_fk) REFERENCES Auxiliar(Id)
);
