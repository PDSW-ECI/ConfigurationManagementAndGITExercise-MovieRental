###Escuela Colombiana de Ingeniería
###Procesos de desarrollo de software – PDSW

Administración de la configuración – Control de versiones con GIT
#Trabajo en parejas

1. Descargue y descomprima el proyecto suministrado (ProyectoBase.zip).
2. Cree una cuenta (para cada integrante del grupo) en GitHUB. En una de las dos cuentas, cree un nuevo repositorio. Invite al usuario de su compañero como colaborador de dicho proyecto.
3. En el directorio raíz del proyecto, crear un archivo .gitignore, en el cual se especifique que el directorio ‘target’ no hará parte del control de versiones (agregue a dicho archivo una línea con: target ).
4. Cree un repositorio local para dicho proyecto, con:
git init .
5. Agregue todos los elementos actuales dentro del repositorio con:
git add .
6. Haga commit de los cambios en el repositorio local, incluyendo un mensaje descriptivo, por ejemplo:
git commit -m "primera revisión del proyecto"
7. Haga push de la rama ‘master’ repositorio local al repositorio creado anteriormente en la organización de GitHub:
git push URL_REPOSITORIO master
8. Rectifique, en la respectiva página Web, que los archivos hayan quedado en el repositorio de GitHub.

9. Entre los integrantes, distribúyanse los roles de autor 1 y autor 2, y realicen las siguientes tareas en computadores diferentes:

	__Autor 1 y 2:__
	
	Clonar el proyecto localmente:
	
	```
	git clone
	```
	
	__Autor 1:__
	
	* Modifica el pom.xml, para que incluya el servidor embebido de Tomcat (agregar en los 'plugins' de la fase 'build'):

		```xml
            <!-- Tomcat embedded plugin. -->
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
                <configuration>
                    <port>8080</port>
                    <path>/</path>
                </configuration>
            </plugin>
	```

	* Commit
	* Push a GitHub
	
	
	
	__Autor 2:__
	
	* Agregar al descriptor de la aplicación Web (web.xml) la configuración que permite habilitar el servlet de PrimeFaces:
	
		```xml
	    <servlet>
	        <servlet-name>Faces Servlet</servlet-name>
	        <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
	        <load-on-startup>1</load-on-startup>
	    </servlet>
	    <servlet-mapping>
	        <servlet-name>Faces Servlet</servlet-name>
	        <url-pattern>/faces/*</url-pattern>
	    </servlet-mapping>
	    <session-config>
	        <session-timeout>
	            30
	        </session-timeout>
	    </session-config>
	    <welcome-file-list>
	        <welcome-file>faces/index.xhtml</welcome-file>
	    </welcome-file-list>	
```
	
	Si para alguno no es posible (por consistencia) hacer el ‘push’, haga un pull a la rama ‘master’ del repositorio en GitHub con ‘rebase’:

	
	```
		git pull --rebase URL_REPOSITORIO master
	```
	
	Al final, todos rectificar que quedan con la última versión respecto al repositorio de GitHUB:
	
	```
	git pull URL_REPOSITORIO master
	```

10. De nuevo, en dos computadores diferentes:

	__Autor 1:__
	* En la clase de pruebas ConsultaTest defina las clases de equivalencia para las pruebal del método de registro de consultas a pacientes.
	* Implementar una prueba para el registro de consultas.
	* Commit
	* Push a GitHub
	
	
	__Autor 2:__

	* En la clase de pruebas PacienteTest defina las clases de equivalencia para las pruebas del método de registro de pacientes.
	* Implementar una prueba para el registro de nuevos pacientes.
	* Commit
	* Push a GitHub



11. Ahora, los dos autores van a trabajar simultáneamente sobre el mismo método de un archivo:

	__Autor 1:__
	* En la interfaz ServiciosPacientes, Corrige la ortografía de la documentación del método registrarNuevoPaciente
	* Commit
	* Push
	
	__Autor 2:__

	* En la interfaz ServiciosPacientes, corrige la documentación de la sección '@Throws' ya que hace referencia a una excepción diferente a la que el método define que podría ser lanzada.
	* Commit
	* Push


	Si para alguno no es posible (por consistencia) hacer el ‘push’, haga un pull a la rama ‘master’ del repositorio en GitHub con ‘rebase’, como en el paso anterior.
En este caso, probablemente no sea posible hacer una ‘mezcla’ automática de los cambios hechos desde dos repositorios diferentes, lo cual se muestra en un mensaje como este:

	![alt text](img/SampleError.png)


	De manera que la acción de --rebase queda inconclusa hasta que se corrijan los conflictos generados. Para este caso, edite el archivo, y ajuste el conflicto, el cual se presenta con el siguiente formato:

	```
<<<<<<< HEAD (commit más reciente del repositorio)
	Cambio obtenido del respositorio externo 
	Mediante el pull --rebase
=======
	Cambio del repositorio local que se intentó 
	combinar con el cambio del repositorio externo.
>>>>>>> comentario del último commit
```

	Una vez generada una versión válida, agregue el cambio con:

	```
git add NombreDelArchivo.java
git rebase --continue
```

	Y posteriormente, haga push a la nuevos cambios al repositorio de GitHUB con push. Al final, todos deben hacer un ‘pull’ para garantizar que estén trabajando sobre la última versión.

12. (Para el Jueves) Implementar la aplicación Web que permita registrar nuevos pacientes, y registrar consultas a para los mismos. Ambas funcionaliadades estarán en dos vistas difernetes (registroconsultas.xhtml, registropacientes.xhtml), de acuerdo con las siguientes especificaciones:
	
	1. Se debe completar la implementación de las pruebas, y hacer los ajustes necesarios en caso de encontrar un defecto en la implementación de 'ServiciosPacientesStub'.
	2. La vista de 'registro de pacientes' debe (1) Mostrar los campos necesarios para registrar un nuevo paciente (y su correspondiente botón de registro), y (2) Mostrar el listado de pacientes existentes junto con un botón de 'registrar cita'. Al oprimirse el botón asociado a uno de los pacientes, se debe redirigir al usuario a la vista del 'registro de citas'.
	3. La vista 'registro de citas', a partir del paciente seleccionado en la vista anterior, debe (1) Mostrar el listado de consultas realizado para el paciente, y (2) Permitir capturar los datos de una nueva consulta a dicho paciente.
	4. Ambas vistas se basarán en el ManagedBean de sesión 'RegistroConsultaBean', el cual -a su vez- hace uso de los 'ServiciosPacientes'.
	5. El desarrollo de ambas vistas debe quedar distribuido entre los dos desarrolladores de la siguiente manera:
	
		* Desarrollador 1: Vista registro paciente.
		* Desarrollador 2: Vista registro consulta.
		* Desarrollador 1 y 2: ManagedBean 'RegistroConsultaBean'.

	Nota. Para ver cómo navegar entre vistas con JSF revise [este enlace.](http://www.tutorialspoint.com/jsf/jsf_page_navigation.htm)
	
13. Entrega:
	1. En los 'logs' de GitHUB debe quedar evidencia de los 'commit' realizados por cada autor, y en computadores diferentes (esto es verificable). Para esto, no olvide configurar su usuario antes de hacer los commits:

		```
		$ git config --global user.name "John Doe"
		$ git config --global user.email johndoe@example.com
	```
	2. Subir en el espacio de moodle un archivo de texto que tenga los integrantes, qué rol se asignó a cada uno (desarrollador 1/ desarrollador 2) y la URL del repositorio en GitHUB.


###Referencias adicionales:

	[No Changes - Did You Forget to Use ‘Git Add’?](http://wholemeal.co.nz/blog/2010/06/11/no-changes-did-you-forget-to-use-git-add/)

	[Git – rebasing – step by step](http://gitforteams.com/resources/rebasing.html)

	[Guía rápida GIT](http://rogerdudler.github.io/git-guide/)
