# Maternidad
create table doctor(
	id_doctor int primary key not null,
	nombre_doc varchar,
	cedula varchar,
	especialidad character varying);
	
	create table cliente(
	id_cliente int primary key not null,
	cedula varchar,
	nombre_pacientes varchar,
	apellido varchar,
	direccion varchar,
	telefono character varying,
	fecha_de_registro date,
	id_doctorpk int,
	foreign key(id_doctorpk)references doctor(id_doctor));
	
	create table medicina(
	id_medicina int primary key not null,
	descripcion_medicina varchar,
	unidad varchar,
	presentacion varchar,
	vacuna varchar,
	fecha_de_dosis date,
	dosis character varying,
	id_clientepk int,
	id_doctorpk int,
	foreign key(id_clientepk)references cliente(id_cliente),
	foreign key(id_doctorpk)references doctor(id_doctor));
	
	create table prematuro(
	id_prematuro int primary key not null ,
	nombre_bebe character varying,
	fecha_de_ingreso date,
	genero varchar,
	id_medicinapk int,
	foreign key(id_medicinapk)references medicina(id_medicina));
	
	create table consulta(
	id_consulta int primary key not null,
	nombre_pacientes varchar,
	control_visitas_fechas date,
	visita_1 varchar,
	visita_2 varchar,
	visita_3 varchar,
	visita_4 varchar,
	visita_5 varchar,
	id_clientepk int,
	id_prematuropk int,
	foreign key(id_clientepk)references cliente(id_cliente),
	foreign key (id_prematuropk)references prematuro(id_prematuro));
	
	insert into doctor values
	(01,'Dr.Samuel','1304800259','pediatra'),
	(02,'Dr.Enrique','1305956211','pediatra'),
	(03,'Dr.Miguel','1309632887','pediatra'),
	(04,'Dr.Jose','1304800251','pediatra'),
	(05,'Dr.Jimmy','1308598773','pediatra');
	select * from doctor;
	
	insert into cliente values
	(489,1306945628,'selena','zambrano','calle16av29',0985741259,'03/03/2020',01),
	(569,1316689742,'maria','vera','calle12av18',095622214,'05/01/2020',02),
	(751,1305520111,'belen','sanchez','calle11av10',0856412433,'07/02/2020',03),
	(165,1318927888,'belinda','rodriguez','calle24av12',0956622571,'02/06/2020',04),
	(395,1305522162,'roxana','velez','calle26av8',0936555987,'20/08/2020',05);
	select * from cliente;
	
	insert into medicina values
	(011,'tetano','miligramos','frasco','hepatitis_b','23/07/2020','1dosis',489,01),
	(012,'difteria','miligramos','frasco','hib','24/01/2020','3dosis',569,02),
	(013,'pertussis','miligramos','frasco','pertussis','22/02/2020','5dosis',751,03),
	(014,'hib','miligramos','tetano','frasco','25/06/2020','4dosis',165,04),
	(015,'poliomielitis','miligramos','frasco','difteria','30/08/2020','2dosis',395,05);
	select * from medicina;
	
	insert into prematuro values
	(0255,'samuel','11/03/2020','masculino',011),
	(0528,'issac','10/01/2020','masculino',012),
	(0782,'liam','14/02/2020','masculino',013),
	(0236,'camila','15/06/2020','femenino',014),
	(0896,'salome','16/08/2020','femenino',015);
	select * from prematuro;
	
	insert into consulta values
	(489,'selena','03/03/2020','23-12-2020','03-07-2020','21-08-2020','9-09-2020','05-10-2020',489,0255),
	(569,'maria','05/01/2020','22-03-2020','05-06-2020','20-09-2020','6-10-2020','03-05-2020',569,0528),
	(751,'belen','07/02/2020','25-06-2020','08-032020','19-02-2020','08-02-2020','09-08-2020',751,0782),
	(165,'belinda','02/06/2020','02-07-2020','07-04-2020','21-04-2020','05-09-2020','20-06-2020',165,0236),
	(395,'roxana','20/08/2020','19-09-2020','10-07-2020','21-07-2020','01-05-2020','01-09-2020',395,0896);
	select * from consulta;
	
	--CONSULTAS--
	
	select cliente.nombre_pacientes,visita_1,visita_2,visita_3,visita_4 from consulta
	inner join cliente on id_cliente=id_clientepk order by nombre_pacientes;
	
	select nombre_bebe,vacuna,dosis from prematuro
	inner join medicina on id_medicina=id_medicinapk order by nombre_bebe;
	
	select doctor.nombre_doc, cliente.cedula,cliente.nombre_pacientes,fecha_de_dosis from medicina
	inner join doctor on id_doctor=id_doctorpk
	inner join cliente on id_cliente=id_clientepk order by nombre_doc desc;
	
	select nombre_doc,descripcion_medicina,fecha_de_dosis,dosis from medicina
	inner join doctor on id_doctor=id_doctorpk order by nombre_doc asc;
