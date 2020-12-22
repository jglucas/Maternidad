# Maternidad
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
